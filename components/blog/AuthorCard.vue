<template>
  <div class="max-w-sm mx-auto">
    <div v-if="author" class="card bg-base-100 shadow-xl hover:shadow-2xl transition">
      <figure class="px-6 pt-6">
        <img v-if="author"
             :src="getMediaUrl(author,'avatar')"
             alt="Author Avatar"
             class="rounded-full w-32 h-32 object-cover border-4 border-base-200"
        >
      </figure>

      <div class="card-body items-center text-center">
        <h2 class="card-title text-lg font-bold">
          {{ author.name }}
        </h2>
        <p class="text-base-content/70 text-sm md:text-base">
          {{ author.job }}
        </p>

      </div>
    </div>
  </div>
</template>

<script setup>
import {getMediaUrl, usePocketBase} from "@/utils/pocketbase"

const props = defineProps({
  identifier: {
    type: String, required: true
  }
})

const author = ref({});
const pb = usePocketBase();

const load = async ()=>{
  author.value = await pb.collection("blog_articel_authors").getOne(props.identifier);
}

watch(()=>props.identifier, () => {
  load();
})
</script>
