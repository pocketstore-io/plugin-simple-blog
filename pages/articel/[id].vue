<script setup lang="ts">
import {usePocketBase} from "@/utils/pocketbase";
import {useRoute} from "vue-router";
import AuthorCard from "@/components/blog/AuthorCard.vue";
import ArticelCommentForm from "@/components/blog/ArticelCommentForm.vue";
import ArticelRelated from "@/components/blog/ArticelRelated.vue";
import ArticelComments from "@/components/blog/ArticelComments.vue";

const route = useRoute();
const item = ref({});
const author = ref({});
const pb = usePocketBase();

const load = async () => {
  pb.autoCancellation(false)
  item.value = await pb.collection('blog_articels').getFirstListItem('slug="' + route.params.id.replace('.html', '') + '"');
  author.value = await pb.collection('blog_articel_authors').getOne(item.value.author);
  useSeoMeta({
    title: item.value.name,
    description: item.value.description,
  })
}
const markdown = computed(() => {
  return item.value.content;
})

onMounted(load)
</script>

<template>
  <section class="bg-white px-3 py-3 w-full">
    <section class="headline flex flex-col md:flex-row md:justify-between">
      <h2 class="font-bold text-xl">Artikel: {{ item.name }}</h2>
      <section class="author">
        von <a href="/" class="font-bold text-primary">{{ author.name }}</a> <br class="md:hidden">
        - erstellt am <b>{{ new Date(item.created).toLocaleDateString('de') }}</b>
      </section>
    </section>
    <hr class="mb-6">
    <div class="prose-sm" v-html="markdown"></div>
    <AuthorCard
        :identifier="item.author"
    />
    <ArticelCommentForm/>
    <ArticelComments :articel="route.params.id.replace('.html', '')"/>
    <ArticelRelated/>
  </section>
</template>