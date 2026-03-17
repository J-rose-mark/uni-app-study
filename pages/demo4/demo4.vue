<template>
  <view>
    姓名：{{name}}-{{age}}
    <!-- // ref="scroll" 是 Vue 模板引用，用于获取组件 / DOM 实例； -->
    <scroll-view scroll-y="true" ref="scroll">
      <view></view>
    </scroll-view>
  </view>
</template>
<!-- onLoad = 加载数据：拿参数、请求接口，不能操作视图 -->
<!-- onReady = 操作视图：页面渲染完毕，可以用 ref 操作组件 / DOM；
顺序：onLoad 先跑 → 渲染页面 → onReady 最后跑。 -->
<!-- 千万不要在 onLoad 里操作 ref
一定会报错 Cannot read property 'scrollTo' of null，因为组件还没渲染出来；
接收参数只能用 onLoad
onReady 拿不到页面跳转的 options 参数；
页面返回后重新进入
onLoad 不会重复执行（页面被缓存），想重复执行逻辑用 onShow -->

<!-- 小程序：onLoad 拿参数，onShow 刷数据，onReady 改页面，onHide 清垃圾；
Vue3：onMounted 就是渲染完成，干小程序 onReady 的活； -->
<script setup>
  import {
    ref,
    onMounted
  } from 'vue';
  import {
    onLoad,
    onReady,
    onShow,
    onHide,
    onUnload
  } from '@dcloudio/uni-app';
  const name = ref(null);
  const age = ref(null);
  const scroll = ref(null);
  onLoad((e) => {
    name.value = e.name,
      age.value = e.age,
      console.log(e)
  })
  onReady(() => {
    console.log("onReady函数")
  })
  onShow(() => {
    console.log("onShow函数")
  })
  onHide(() => {
    console.log("onHide函数")
  })
  onMounted(() => {
    console.log("onMounted函数")
  })
  onUnload(() => {
    console.log("onUnload")
  })
</script>

<style lang="scss">

</style>