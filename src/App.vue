<template>
  <div class="container">
    <div class="darkmode" @click="toggleDark()">
      <i v-if="isDark" class="iconfont icon-yueliang" ></i>
      <i v-else class="iconfont icon-ai250"></i>
    </div>
    <main>
      <!-- <Header @update:word-value="handleChange"></Header> -->
      <Header v-model="searchWord"></Header>
      <Definition :searchWord="searchWord"></Definition>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Header from './components/Header.vue'
import Definition from './components/Definition.vue'
import { toggleDark, isDark } from './composables';
const searchWord = ref()

// watch(searchWord,(newValue)=>{
//   console.log(newValue)
// })
//vue3可以直接使用v-model接受子组件传来的值,无需自定义事件
// const handleChange = (value)=>{
//   word.value = value
// }
</script>


<style lang="scss" scoped>
div.container {
  height: 100vh;
  overflow: hidden;

  // background-color: #282c34;
  main {
    max-width: 1000px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    // color:white;
    padding: 1rem
  }
  .darkmode{
    padding: 10px;
    
  }
}
</style>
