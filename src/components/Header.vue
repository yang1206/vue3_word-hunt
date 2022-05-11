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

</style>
