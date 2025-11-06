<template>
  <section class="grid grid-cols-6 gap-3">
    <div class="col-span-2 md:col-span-6">
      <img :src="url +
            '/api/files/' +
            customer.collectionId +
            '/' +
            customer.id +
            '/' +
            customer.avatar" class="border-2 border-black w-24" alt="">
    </div>
    <div class="col-span-4 md:col-span-6 text-sm">
      {{$t('labels.name')}}: <b>{{customer.name}}</b><br>
      {{$t('labels.memberSince')}}: <b>{{new Date(customer.created).toLocaleDateString('de')}}</b> <br>
      {{$t('labels.comment')}}: <b>{{counter}}</b>
    </div>
  </section>
</template>

<script setup lang="ts">
import {usePocketBase,usePocketBaseUrl} from "@/util/pocketbase";

const props = defineProps({
  identifier: {required: true, type: String}
});

const customer = ref({});
const pb = usePocketBase()
const url = usePocketBaseUrl()
const counter = ref(1234);

const load = async () => {
  customer.value = await pb.collection('customers').getOne(props.identifier);
}

onMounted(load);
</script>