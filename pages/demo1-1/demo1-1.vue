<template>
  <view>
    <Slots-layout>
      <view class="box1">
        box1
      </view>
      <view class="box2">
        box2
      </view>
    </Slots-layout>
  </view>
</template>

<script setup>

</script>

<style lang="scss">
  .box1 {
    width: 100px;
    height: 100px;
    background-color: pink;
  }

  .box2 {
    width: 130px;
    height: 130px;
    background-color: green;
  }
</style>