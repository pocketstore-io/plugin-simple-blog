<template>
  <section class="mt-6">
    <section class="grid grid-cols-6 gap-3 bg-gray-300 border-2 border-black">
      <div class="col-span-2">
        <img :src="url+'/api/files/'+props.data.collectionId+'/'+props.data.id+'/'+props.data.avatar" alt="">
      </div>
      <div class="col-span-4 prose-sm">
        <h3 class="font-bold mt-2">Author: {{ props.data.name }}</h3>
        <p class="block pr-3">{{ props.data.description }}</p>
        <section class="social-media-icons">
          <h5 class="font-bold">Kontakt und Social Media</h5>
          <hr class="!my-2">
          <section class="grid grid-cols-10 gap-3">
            <div class="col-span-2 text-center">
              <a href="/">
                <font-awesome-icon :icon="['fas', 'envelope']"></font-awesome-icon>
              </a>
            </div>
            <div class="col-span-2 text-center">
              <a href="/">
                <font-awesome-icon :icon="['fab', 'whatsapp']"></font-awesome-icon>
              </a>
            </div>
            <div class="col-span-2 text-center">
              <a href="/">
                <font-awesome-icon :icon="['fab', 'github']"></font-awesome-icon>
              </a>
            </div>
            <div class="col-span-2 text-center">
              <a href="/">
                <font-awesome-icon :icon="['fab', 'linkedin']"></font-awesome-icon>
              </a>
            </div>
            <div class="col-span-2 text-center"><a href="/">
              <font-awesome-icon :icon="['fab', 'instagram']"></font-awesome-icon>
            </a>
            </div>
          </section>
        </section>
      </div>
    </section>
  </section>
</template>

<script setup lang="ts">
import {usePocketBaseUrl} from "@/util/pocketbase";
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

const props = defineProps({
  data: {type: Object, required: true}
});
const url = usePocketBaseUrl();
</script>