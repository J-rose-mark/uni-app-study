<template>
  <view>
    <Slots-layout>
      <!-- 具名插槽可以指定哪个地方用插槽 -->
      <template v-slot:header>这是header区域</template>
      <template v-slot:main>这是main区域</template>
    </Slots-layout>
    <!-- 条件插槽 -->
    <!-- 用 v-if="$slots.插槽名" 做判断：
    只有插槽真的有内容传入，才渲染插槽外层的包裹容器，
    没传内容时，整个容器连带插槽都不会渲染，
    不会留下空的 DOM 节点。 -->
    <!-- 优点 -->
    <!-- 
    避免 DOM 冗余：不会生成无内容的空 DOM 节点，减少页面渲染负担；
    样式完全可控：杜绝空容器的默认样式（padding、margin、border 等）导致的布局错乱，比如没传 header 时，卡片不会多出一块空白头部；
    组件封装更健壮：子组件自主处理插槽的显隐，不需要父组件额外传参数控制容器的显示隐藏，降低组件使用成本，提升灵活性。 -->

    <!-- 动态插槽 -->
    <!-- 动态插槽，就是让「插槽名」不再写死，而是通过变量 / JS 表达式动态决定，让内容分发的目标位置可以灵活变化，是 Vue 对静态插槽能力的扩展，大幅提升组件的通用性和灵活性。 -->
    <!-- 通用组件、动态渲染、批量处理的场景：动态插槽能极大简化代码，提升组件的复用性和灵活性。 -->

    <!-- 作用域插槽 -->
    <!-- 作用域插槽，就是让「子组件」能把自己内部的数据，传给「父组件」的插槽内容，父组件拿到数据后，可以自定义内容的展示方式，解决了 “父组件想用子组件里的数据，但普通插槽拿不到” 的痛点。 -->
    <!-- 用法 -->
    <!-- 组件中需要在<slot>中将需要传递的参数传过去 -->
    <!-- 父级中需要v-slot自定义一个名来接受传递过来的数据 -->
    <!-- 如果是具名插槽传的话，则不用自定义一个名来接受，可以直接解构 -->
    <!-- 子组件：通用列表 List.vue -->
    <!--   <template>
      <div class="list">
        <div v-for="(item, index) in listData" :key="item.id">
          <slot :item="item" :index="index"></slot>
        </div>
      </div>
    </template> 
    父组件
    <List v-slot="{ item, index }">
      <div>第{{ index }}项：{{ item.name }} - {{ item.age }}岁</div>
    </List>-->
  </view>
</template>

<script setup>

</script>

<style lang="scss">

</style>