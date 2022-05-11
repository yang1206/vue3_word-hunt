<template>
  <header>
    <h2 class="title">{{ wordValue ? wordValue : 'Word Hunt' }}</h2>
    <div class="input-wrap">
      <input type="text" :class="{ dark: isDark }" placeholder="搜索单词" v-model="wordValue"
        @input="$emit('update:modelValue', $event.target.value)">
    </div>
  </header>
</template>

<script setup>
import { isDark } from '../composables';
import { ref } from 'vue'
const wordValue = ref()
defineEmits(['update:modelValue'])
</script>

<style lang="scss" scoped>
header {
  height: 30vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  h2 {
    font-size: 7vw;
    font-weight: 100;
    @media (max-width: 1000px) {
      font-size: 11vw;
    }
  }

  .input-wrap {
    input {
      width: 50vw;
      border: none;
      // background-color: $bg;
      border-bottom: 1px solid rgba(197, 188, 188);
      padding: 5px;
      color: white;
      font-size: 18px;
      &:focus {
        outline: none;
        // border-bottom: 1px solid white;
      }
      &::placeholder {
        // color: rgba($color: #fff, $alpha: 0.6);
      }
    }
  }
}
</style>
