<template>
  <section class="bg-gray-300 border-2 border-black my-3 px-3 py-3">
    <section class="grid grid-cols-6 gap-3">
      <div v-if="pb.authStore.isValid" class="col-span-6 md:col-span-2">
        <ArticelCustomer :identifier="pb.authStore.record.id"/>
      </div>
      <div v-else class="col-span-6 md:col-span-2 block text-center mt-3">
        <span>{{$t('note.notLoggedIn')}} </span> <br>
        <button @click="open = true" class="btn btn-sm btn-primary mt-3 mb-3">
          {{$t('actions.login')}}
        </button>

        <input type="checkbox" v-model="open" class="modal-toggle" />
        <div class="modal mx-3" role="dialog">
          <ModalLogin />
          <label class="modal-backdrop" @click="open=false">{{$t('labels.close')}}</label>
        </div>
      </div>
      <div v-if="pb.authStore.isValid" class="col-span-6 md:col-span-4">
        <div v-if="!successfullWriten">
          <ArticelWriteComment @geschrieben="successfullWriten = true" />
        </div>
        <div v-else>
          <div class="alert alert-success text-center mt-3 mb-3">
            {{$t('toast.success.comment')}}
          </div>
        </div>
      </div>
    </section>
  </section>
</template>
<script setup lang="ts">
import ArticelCustomer from "~/components/blog/ArticelCustomer.vue";
import {usePocketBase} from "~/util/pocketbase";
import {useLocalStorage} from '@vueuse/core'
import ArticelWriteComment from "~/components/blog/ArticelWriteComment.vue";
import ModalLogin from "~/components/modal/Login.vue";

const pb = usePocketBase();
const successfullWriten = ref(false);
const open = useLocalStorage('modal-login',false,{})
</script>