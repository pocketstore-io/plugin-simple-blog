<template>
  <section class="bg-gray-300 border-2 border-black my-3 px-3 py-3">
    <section class="grid grid-cols-6 gap-3">
      <div v-if="pb.authStore.isValid" class="col-span-6 md:col-span-2">
        <ArticelCustomer :identifier="pb.authStore.record.id"/>
      </div>
      <div v-else class="col-span-6 md:col-span-2 block text-center mt-3">
        <span>Nicht eingeloggt, zum </span> <br>
        <button @click="open = true" class="btn btn-sm btn-primary mt-3 mb-3">
          Login
        </button>

        <!-- Put this part before </body> tag -->
        <input type="checkbox" v-model="open" class="modal-toggle" />
        <div class="modal mx-3" role="dialog">
          <ModalLogin />
          <label class="modal-backdrop" @click="open=false">schlie0en</label>
        </div>
      </div>
      <div v-if="pb.authStore.isValid" class="col-span-6 md:col-span-4">
        <h4 class="font-bold">
          Kommentar schreiben
        </h4>
        <textarea class="textarea"></textarea>
        <section class="actions flex justify-end mt-3">
          <button class="btn btn-primary">abschicken</button>
        </section>
      </div>
    </section>
  </section>
</template>
<script setup lang="ts">
import ArticelCustomer from "~/components/blog/ArticelCustomer.vue";
import ModalLogin from "~/components/modal/Login.vue";
import {usePocketBase} from "~/util/pocketbase";
import {useLocalStorage} from '@vueuse/core'

const pb = usePocketBase();
const open = useLocalStorage('modal-login',false,{})
</script>