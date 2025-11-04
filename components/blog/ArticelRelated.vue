<template>
  <section class="grid grid-cols-6 gap-3 mt-3">
    <div v-for="item in items" class="col-span-6 md:col-span-2">
      <PluginCard :identifier="item.id" />
    </div>
  </section>
</template>
<script setup lang="ts">
import PluginCard from "@/components/PluginCard.vue";
import {usePocketBase} from "@/util/pocketbase";

const items = ref([]);

const pb = usePocketBase();

const load = async () =>{
  items.value = (await pb.collection('plugins').getList(1,3,{})).items;
}
onMounted(load)
</script>