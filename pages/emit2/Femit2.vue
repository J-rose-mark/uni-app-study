<template>
  <view class="box" :style="{background:color,fontSize:size +'px'}">
    <emits @add="Onadd" @onChange="change"></emits>
  </view>
</template>
<!-- $emit 是 Vue 组件通信的核心 API，核心作用是：子组件触发一个自定义事件，同时携带数据，实现「子组件 → 父组件」的单向通信，和父传子的 props 形成父子组件通信的闭环。 -->
<!-- 事件监听的唯一性：$emit 触发的自定义事件，只会被直接父组件捕获，不会像原生 DOM 事件一样向上冒泡，父组件必须显式用 @事件名 监听才能响应。 -->
<!-- 命名规范：Vue3 强烈推荐自定义事件名使用 短横线命名（kebab-case），比如 increase-by，和 HTML 属性规范保持一致，避免大小写兼容问题。 -->
<!-- 多参数传递：$emit 支持传递多个参数，例如 emit('update-user', name, age, gender)，父组件的监听函数可以按顺序接收：@update-user="(name, age, gender) => {}"。 -->
<!-- 事件校验：defineEmits 支持对传递的参数做类型校验，提升代码健壮性 -->
<!-- 和原生事件的区别：@click 是浏览器自带的原生 DOM 事件，而 @increase-by 是我们通过 $emit 自定义的事件，自定义事件必须通过 $emit 触发才会生效。 -->
<script setup>
  import {
    ref
  } from 'vue'
  const color = ref('#eee');
  const size = ref(45)
  const Onadd = function(e) {
    console.log(e)
    color.value = "#" + String(e).substring(3, 6)
  }
  const change = function(e) {
    size.value = e
  }
</script>

<style>
  .box {
    width: 200px;
    height: 200px;
  }
</style>