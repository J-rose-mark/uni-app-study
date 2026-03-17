<template>
  <view>
    <!-- 父组件接受子组件的信息需要用ref来接受，后面可以自定义 -->
    <defineEpose ref="epose"></defineEpose>
    <button @click="onchange">改变子组件的值</button>
    <navigator open-type="reLaunch" url="/pages/demo4/demo4?name=王五&age=20">逆转吧</navigator>
  </view>
</template>
<!-- defineExpose的作用 -->
<!-- 将子组件内部的属性、方法，主动暴露给父组件访问。 -->
<script setup>
  import {
    ref
  } from 'vue'
  const epose = ref(null)
  console.log('打印瞬间的 epose.value：', epose.value)
  // 为什么打印出来的不是null
  // 因为setup 同步打印时，epose.value 就是 null，没有任何问题；
  // 看到 12 是因为浏览器控制台异步展开对象，展示的是挂载后的最新值；
  // 用 ref 绑定子组件，必须等组件挂载完成，epose.value 才会变成子组件实例。
  console.log(epose)
  const onchange = function() {
    epose.value.updateCount()
  }
</script>

<style lang="scss">

</style>