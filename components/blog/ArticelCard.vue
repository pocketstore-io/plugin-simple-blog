<script setup lang="ts">
import {usePocketBase} from "@/util/pocketbase";

const props = defineProps({
  identifier: {type: String, required: true}
});

const tags = ref([]);
const item = ref({});
const pb = usePocketBase();

const load = async () => {
  pb.autoCancellation(false)
  item.value = await pb.collection('blog_articels').getOne(props.identifier);
  tags.value = (await pb.collection('blog_articel_tags').getList(1, 10, {
    filter: 'articel="' + props.identifier + '"'
  })).items;
}

onMounted(load)
</script>

<template>
  <div class="card bg-gray-400 shadow-sm">
    <figure>
      <img
          src="https://img.daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.webp"
          alt="Shoes"/>
    </figure>
    <div class="card-body">
      <h2 class="card-title">
        {{ item.name }}
        <div v-if="item.isNew" class="badge badge-secondary">{{ $t('labels.new') }}</div>
      </h2>

      <p>{{ item.description }}</p>
      <div class="card-actions">
        <a v-for="tag in tags" :href="'/de/blog/tag/'+tag.tag.toLowerCase()" class="badge badge-outline border-white text-white font-bold">
          {{tag.tag}}
        </a>
      </div>
      <section class="card-actions flex justify-end space-x-3">
        <a :href="'/de/articel/'+item.slug+'.html'" class="btn btn-primary">
          {{$t('actions.readMore')}}
        </a>
      </section>
    </div>
  </div>
</template>