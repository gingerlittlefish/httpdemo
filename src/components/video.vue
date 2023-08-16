<template>
    <div v-if="data" class="boxMain">
    <div v-for="item in data" class="listbox" >
       
        <div class="articleTitle" @click="handleClick(item)">{{ item.title }}</div>
        <div class="author">author:{{ item.author.nickname }}</div>
      
    </div>
    </div>
  </template>
  
/**
*  1. 通过props决定list显示的长度，size最多为20，需要校验
*  2. 暴露出上一页下一页方法，可以加载对应数据
*  3. 当点击item后通过自定义事件通知调用者  
*/


  <script setup>
  import axios from 'axios'
  import { onMounted,ref ,watch,reactive} from 'vue';
  
  const data = ref()
   
  
//   const props = defineProps(['limit'])
  const props = defineProps({
    size:Number,   
    page:Number,
    Id:Number
  })



  const propsRef = reactive(props)
  const emit = defineEmits(['alertName','showArticle'])
  
  function changePage(page){
    axios.get(`https://api-prod.wisburg.com/v1/article/flow`,{
          params:{
              limit:props.size,
              page:page
          }
    })
    .then(res=>{
        data.value = res.data.data.list
      })
  }

  const handleClick = (it) => {
    emit('alertName',it)
    emit('showArticle',it.id)
  };

  changePage()

  watch(()=>props.page,(newValue)=>{
    // changePage(newValue)
    // axios.get(`https://api-prod.wisburg.com/v1/article/flow`,{
    //       params:{
    //           limit:props.size,
    //           page:newValue
    //       }
    // })
    //   .then(res=>{
    //   data.value = res.data.data.list
    //   })
  }) 

  defineExpose({
    changePage
  })

  
  </script>
  
  <style>
  .boxMain{
    margin: 0 auto;
    background-color:rgb(220, 230, 221) ;
  }

  .boxMain:hover{
      background-color: #23a354;
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