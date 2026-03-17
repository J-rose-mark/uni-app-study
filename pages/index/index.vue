<template>
  <!-- <Props username="微风铃铃" avatar="../../static/pic1.png"></Props>
  <Props username="微风铃铃" avatar="../../static/pic2.png"></Props>
  <Props :username="name" avatar="../../static/pic3.png"></Props> -->
  <Props v-for="(item,index) in userinfo" :obj="item"></Props>

</template>

<script setup>
  import {
    ref
  } from 'vue';
  // const name = '网主'
  const userinfo = ref([{
    name: "张三",
    avatar: "/static/pic2.png",
  }, {
    name: "张三",
    avatar: "/static/pic3.png",
  }, {
    name: "张三",
    avatar: "/static/pic4.png",
  }, ])
</script>

<style lang="scss">

</style>