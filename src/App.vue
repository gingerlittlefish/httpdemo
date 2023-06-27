<template>
  <template v-if="data">
  <div v-for="item in data">
  {{ item.title }}
  </div>
  </template>
</template>

<script setup>
import axios from 'axios'
import { onMounted,ref } from 'vue';

const data = ref()

  axios.get('https://api-prod.wisburg.com/v1/article')
       .then(res=>{
        data.value = res.data.data.title
       }).then(res=>{
        console.log(res)
  })


</script>

<style>

</style>