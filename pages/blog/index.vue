<template>
  <section class="bg-white px-3 py-3">
    <section class="grid grid-cols-6 gap-3">
      <div class="col-span-6">
        <h2 class="font-bold text-lg">
          {{$t('blog.headline')}}
        </h2>
      </div>
      <div v-if="items.length > 0" v-for="item in items" class="col-span-6 sm:col-span-3 lg:col-span-2">
        <ArticelCard :identifier="item.id"/>
      </div>
      <div v-else class="col-span-6">
        <section class="alert alert-error">
          {{$t('blog.no-articels')}}
        </section>
      </div>
    </section>
  </section>
</template>
<script setup lang="ts">
import ArticelCard from "@/components/blog/ArticelCard.vue";
import {usePocketBase} from "@/utils/pocketbase";
import {addBreadcrumb, clearBreadcrumbs} from '@/utils/breadcrumb'

const items = ref([]);

const pb = usePocketBase()

const load = async () => {
  items.value = (await pb.collection('blog_articels').getList(1, 9, {
    sort: '-created'
  })).items;
}

onMounted(() => {
  load();
  clearBreadcrumbs();
  addBreadcrumb({
    code: 'blog',
    icon: 'rss',
    link: '/de/blog',
  })
});
</script>