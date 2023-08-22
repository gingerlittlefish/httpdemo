<template>
    <div>
      <div class="tab-buttons">
        <button v-for="(tab, index) in tabs" :key="index" @click="currentTab = index">{{ tab }}</button>
      </div>
      <div class="tab-content">
        <div v-for="(tab, index) in tabs" :key="index" v-show="currentTab === index">
          <p>{{ tab }}</p>
        </div>
      </div>
    </div>
  </template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const tabs = ['文章', '视频'];
    const currentTab = ref(0);
    return { tabs, currentTab };
  }
};
</script>

<style>
.tab {
    display: flex;
    width: 100%;
    height: 60px;background-color: #333;
    color: aliceblue;
}
</style>