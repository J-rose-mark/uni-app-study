<template>
  <view>
    子组件{{epose}}
    <view></view>
  </view>
</template>

<script setup>
  import {
    onMounted,
    ref
  } from 'vue'
  const epose = ref(12)
  const updateCount = function() {
    epose.value++
  }
  onMounted(() => {
    console.log(epose.value)
  })
  defineExpose({
    epose,
    str: "x",
    updateCount
  })
</script>

<style lang="scss">

</style>