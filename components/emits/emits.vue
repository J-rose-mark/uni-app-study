<template>
  <input type="text" @input="onInput" />
  <view>
    <button @click="change">按钮</button>
    这是一个字
  </view>
</template>

<script setup>
  import {
    ref
  } from 'vue'
  const emit = defineEmits([
    "add",
    "onChange"
  ])
  const num = ref(2)

  function onInput(e) {
    emit("onChange", e.detail.value)
  }

  function change() {
    emit("add", Math.random())

  };
</script>

<style lang="scss" scoped>
  input {
    border: 1px solid pink;
    padding: 10px;
    background-color: #eee;
  }
</style>