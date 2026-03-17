<template>
  <!-- Prop组件的使用 -->
  <view class="Userinfo">
    <image :src="obj.avatar" mode="aspectFill" class="avatar"></image>
    <view class="uesrname">
      {{obj.name}}
    </view>
  </view>
</template>

<script setup>
  // 组件通信，这里是子组件，需要给个标识，方便父组件传递信息过来
  // 子组件只读，不能修改父组件里的信息
  //子组件读取父组件里的信息需要解构
  // props是单向数据流，非要用这个改变数据的话，只能把数据另出来
  // 传字符串、数组和对象的用法不同
  import {
    computed,
    ref
  } from 'vue';
  // const props = defineProps(['username', 'avatar'])
  // console.log  (props)
  defineProps({
    obj: {
      type: Object,
      default () {
        return {
          name: "匿名",
          avatar: "/static/pic2.png"
        }
      }
    }
  })
</script>
<!-- scoped作用使得这个组件的样式只在组件中生效 -->
<style lang="scss" scoped>
  .Userinfo {
    width: 100%;
    height: 200px;
    background-color: #eee;
    align-items: center;
    justify-content: center;
    display: flex;
    flex-direction: column;
    border: 1px solid #fff;

    image {
      width: 100px;
      height: 100px;
      border-radius: 35%;
    }

    .username {
      padding: 10px 0;
      font-size: 30px;
    }
  }
</style>
<!-- 组件的优势是可以统一修改， -->