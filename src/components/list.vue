<template>
    <div v-if="data" class="boxMain">
    <div v-for="item in data" class="listbox" >
       
        <div class="articleTitle">{{ item.title }}</div>
        <div class="author">author:{{ item.author.nickname }}</div>
      
    </div>
    </div>
  </template>
  
  <script setup>
  import axios from 'axios'
  import { onMounted,ref } from 'vue';
  
  const data = ref()
    
  axios.get('https://api-prod.wisburg.com/v1/article/flow')
         .then(res=>{
          data.value = res.data.data.list
         })
  
  
  
  </script>
  
  <style>
  .boxMain{
    margin: 0 auto;
  }
  .listbox{
    padding: 12px 0 20px;
  }

  .articleTitle{
    padding: 10px 20px;
  }

  .author{
    padding: 20px 20px;
  }
  </style>