<template>
  <div class="box">
  <button @click="switchList">切换列表</button>
    <articleDetail :id="articleId"></articleDetail>
    <list ref="compList" :size="3" :page="pageNum" @alertName="showTitle" @showArticle="handleShowArticle"></list>
    <video></video>
    <button @click="prev">上一页</button><button @click="next">下一页</button>
  </div>

</template>
/**
 * 1. 点击列表item后获取点击item并渲染对应的文章
 * 2. 将item的id传入文章组件用于获取文章详情
 * 3. 文章详情组件中新增下一篇按钮，点击后显示下一篇内容，如果没有下一篇则刷新下一页的列表获取最新的一个
 * 4. 父组件收到事件后决定是否需要加载新的列表，并获取下一篇文章id给文章组件 
 */
<script setup>
import articleDetail from './components/articleDetail.vue'
import list from './components/list.vue'
import video from './components/video.vue'
import { onMounted,ref } from 'vue';
const randomSize = ref(Math.round(Math.random()*10))
const compList = ref()
const pageNum = ref(1)
const articleId = ref()
const showTab = ref()



function prev(){
  if (pageNum.value > 1) {
    pageNum.value -= 1
  }
};
function next() {
  pageNum.value += 1 
  compList.value.changePage(pageNum.value)
};

function showTitle(n) {
  alert(`${n.title}`)
};

function handleShowArticle(param) {
  articleId.value = param
}

function switchList(){

}

</script>

<style scoped>
.box{
  margin: 0 auto;
  
}
</style>