<template>
  <h4 class="font-bold">
    {{$t('actions.writeComment')}}
  </h4>
  <textarea v-model="comment" :placeholder="$t('placeholder.comment')" class="textarea border-2 border-black w-full"></textarea>
  <section class="actions flex justify-end mt-3">
    <button @click="send()" class="btn btn-primary">{{$t('actions.send')}}</button>
  </section>
</template>
<script setup lang="ts">
const emit = defineEmits(['geschrieben'])
const comment = ref('');
const router = useRouter();

const send = ()=>{
  emit('geschrieben');
  // TODO store comment in DB
  // Toast Add Message success
  router.go(0)
}
</script>