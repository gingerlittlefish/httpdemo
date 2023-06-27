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


    axios.get('https://api-prod.wisburg.com/v1/popular/articles')
     .then(res=>{
    data.value = res.data.data.title
    }).then(res=>{
        console.log(axios)
    })


</script>

<style>

</style>