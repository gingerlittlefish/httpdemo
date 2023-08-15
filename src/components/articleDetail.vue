<template>
 <div v-if="data" class="boxBody">
    <div v-for="item in data">
    
        <div>{{ item.body }}</div>
      
    </div>
    </div>
</template>

<script setup>
import axios from 'axios'
import { onMounted,ref ,watch,reactive} from 'vue';
const data = ref()
const props = defineProps({
    id:Number
  })

const emit = defineEmits(['showAricle'])

  function showArticle(id){
    axios.get(`https://api-prod.wisburg.com/v1/article/${props.id}`)
    .then(res=>{
        data.value = res.data.data
      }),console.log();
  }
  
  showArticle ()
  
  
</script>

<style>
.boxBody{
    margin: 0 auto;
    background-color:rgb(108, 15, 98) ;
  }
  .listbox{
    padding: 12px 0 20px;
  }
</style>