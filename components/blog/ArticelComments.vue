<template>
<ArticelComment v-for="comment in comments" :data="comment" />
</template>

<script setup lang="ts">

import {usePocketBase} from "@/utils/pocketbase";
import ArticelComment from "./ArticelComment.vue";

const pb = usePocketBase();
const comments = ref([]);
const props = defineProps({
  articel: {required: true, type: String}
});

const load = async () => {
  comments.value = (await pb.collection('blog_articel_comments').getList(1, 10, {
    sort: '-created',
    filter: 'articel.slug="' + props.articel + '"'
  })).items;
}

onMounted(load);
</script>