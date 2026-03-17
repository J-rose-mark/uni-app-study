<template>
  <view>
    <scroll-view scroll-y="true" class="scroll" ref="scroll">
      <view>拿到DOM的数据</view>
    </scroll-view>
  </view>
</template>
<!-- 生命周期 -->
<!-- 父子组件生命周期执行顺序
挂载：父 beforeCreate → 父 created → 父 beforeMount → 子 beforeCreate → 子 created → 子 beforeMount → 子 mounted → 父 mounted
更新：父 beforeUpdate → 子 beforeUpdate → 子 updated → 父 updated
卸载：父 beforeUnmount → 子 beforeUnmount → 子 unmounted → 父 unmounted -->
<!-- DOM 操作时机：
绝对不要在beforeCreate/created/beforeMount里操作 DOM，此时真实 DOM 还未生成，会拿到undefined报错，操作 DOM 必须在onMounted/onUpdated里执行。 -->
<!-- 接口请求时机：
初始数据的接口请求，写在setup里（created）和onMounted里都可以；如果接口返回的数据需要依赖 DOM，必须写在onMounted里。 -->
<!-- 避免死循环：不要在onUpdated里直接修改触发更新的响应式数据，会导致「改数据→触发更新→改数据」的死循环。 -->
<!-- 内存泄漏防护：所有定时器、全局事件监听、第三方实例，必须在onBeforeUnmount里清理，否则组件卸载后依然会占用内存，导致页面越来越卡。
 -->
<!-- 一句话总结核心
DOM：浏览器给 JS 操作页面的接口，改 DOM 就是改页面；
Vue3 生命周期：组件从生到死的全流程，最常用的 3 个场景：
setup里：初始化数据、发起初始接口；
onMounted：操作 DOM、初始化第三方库；
onBeforeUnmount：清理资源，防止内存泄漏。 -->
<script setup>
  import {
    onMounted,
    ref
  } from 'vue'
  const scroll = ref(null);
  onMounted(() => {
    console.log(scroll.value)
  })
</script>

<style lang="scss">

</style>