<script setup lang="ts">
import ArticelCustomer from "./ArticelCustomer.vue";

const props = defineProps({
  data: {required: true, type: Object}
})
</script>

<template>
  <div class="bg-red-400 px-3 py-3">
    <section class="grid grid-cols-6 gap-3">
      <div class="col-span-6 md:col-span-1">
        <ArticelCustomer :identifier="props.data.customer"/>
      </div>
      <div class="col-span-6 md:col-span-5">
        <div class="bg-red-400 px-3 py-3 flex flex-col">
          <h3 class="block font-bold">{{ props.data.headline }}</h3>
          <p class="text-sm">{{ props.data.comment }}</p>
        </div>
      </div>
    </section>
  </div>
</template>