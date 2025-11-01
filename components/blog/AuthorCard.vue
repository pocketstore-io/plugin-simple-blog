<template>
  <section class="mt-6">
    Author Card => {{props.data.name}}
  </section>
</template>

<script setup lang="ts">
const props = defineProps({
  data: {type: Object, required: true}
});
</script>