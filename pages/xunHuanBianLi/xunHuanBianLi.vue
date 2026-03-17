<!-- for与forEach的比较 -->
<!-- forEach不能中途停止，且for性能好 -->
<!-- for不支持异步，会造成异步堵塞，而forEach则不会 -->
<!-- map 可以清洗数据，有返回值，改属性，改值，异步也支持-->
<!-- indexOf：从头开始找索引值，找到之后，就返回下标 -->
<!-- filter要是为真则选出，要是为假则不选 -->
<!-- filter和indexOf两者搭配实现去重
  arrs.filer((item,index,self)=>{
  return self.indexOf(item)===index
}) -->
<!-- filter和map搭配使用
  let newArrs = arrs.filter(item=>{
    return item.id
  }).map(item=>{return{
    ...item,
    author:"..."
  }})-->
<!-- reduce的用法,prev是上一个值,current是当前的值,这两个都是必填的,index是索引 ,最后的零是赋给prev的初始值-->
<!-- let result = arrs.reduce((prev,current,index)=>{
  prev+=current
  if(index === arrs.length-1){
    
  }else{
    
  }
},0) -->
<!-- every，要是全部多为真，才返回true；而some则是有一个满足就返回true
 Object是把obj里面的值数组化
const state = computed(()=>{
  return !Object.values(obj.value).every(item=>item)
})-->
<!-- include 为什么检测不出数组里的数组 
includes() 只能检测「基本数据类型」（字符串、数字、布尔等），不能直接检测「引用数据类型」（数组、对象），
因为数组是引用类型，比较的是内存地址，不是内容。
传入的目标子数组是新创建的数组，和原数组里的子数组内存地址不同，所以 includes 永远检测不到。-->
<template>
  <view>

  </view>
</template>

<script setup>
  let arrs = [...Array(9999999).keys()]
  let total = 0;
  let startTime = Date.now();
  for (let i = 0; i < arrs.length; i++) {
    total += 1;
  }
  let endTime = Date.now();
  let countTime = endTime - startTime;
  console.log("计数----->" + total);
  console.log("消耗时间---->" + countTime);
</script>

<style lang="scss">

</style>