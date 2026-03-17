<!-- 如何引入外部样式 -->
<!-- 第一个种全局样式——app.vue,但是优先级最小 -->
<!-- 第二个，在需要的引入的文件中，在style下@import "@/common/css/style.css" -->
<!-- 第三个，找到uni.scss文件，找到其中想要的样式，复制其键名 -->
<!-- 注意，APP.VUE都是预编译，修改后需要刷新 -->

<!-- static目录 ：
第一个，这个目录存储静态资源，static 目录的文件会被「直接复制」到产物，不会经过编译、压缩、合并等优化处理；
第二个，static里文件越多，加载越慢；
因此，不要将样式文件放入static中，应该自建common目录下-->

<!-- 数据缓存 -->
<!-- uni.setStorageSync & uni.setStorage(异步)-->
<!-- 用法：
 uni.setStorageSync('name', '李四');
 let myName = uni.getStorageSync("name")-->

<!-- 数据删除 -->
<!-- uni.removeStorageSync(KEY)-->
<!-- 全部清除：uni.clearStorageSync("name") -->

<!-- ⭐网络请求 -->
<!-- uni.request(){} -->
<!-- 用法：
第一种：
function request(){
uni.request({
url:网址＋接口；
sunccess:res=>{
arrs.value = res.data   这里接受数据
})
}
第二种
function request(){
uni.request({
url:网址＋接口
}).then(res =>{
arrs.value = res.data
})
}
第三种：异步同步化
async function request(){
  let res = await uni.request({
    url:接口
  })
  arr.value = res.data
}
 -->
<!-- request的参数 -->
<!-- header HTTP请求头-->
<!--附带给服务器的附加信息：我是谁、我发的是什么格式数据，怎么处理 -->
<!-- 这是最核心的用途！登录后服务器会给你一个 token，你必须把 token 放在 header 里传给服务器，否则服务器不知道你是已登录的合法用户。
 用户登录：输入账号、密码，点登录按钮
 请求登录接口：前端把账号密码发给后端
 后端验证返回：后端核对账号密码正确 → 生成 token 返给前端
 前端存储：把 token 存在本地，之后所有接口都带着它-->
<!-- header: {
  // 标准的身份验证写法：Bearer + 空格 + token值
  Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...'
} -->
<!-- 声明数据格式：  
 header: {
   'Content-Type': 'application/json'
 }-->
<!-- 自定义业务标识
 header: {
   'Client-Version': '1.0.0',
   'Device-Type': 'android'
 }-->
<!-- 同步or异步 -->
<!-- 异步 -->
<!-- JS的本质是单线程 + 多线程环境 + 事件循环 (Event Loop) -->
<!-- 异步：第一行步后，但是第二行代码依赖第一步的结果，而第三行代码依赖于第二行代码的结果 -->
<!--回调地狱如下：回调地狱的本质，不是 “依赖上一步”，而是【代码嵌套层级爆炸 + 可读性 / 维护性崩盘】 
  getData(){
    //获取列表id
    uni.request({
      url:接口,
      success:res=>{
        let id = res.data[0].id
        //根据分类id获取该分类下的所有文章
        uni.request({
          url:api，
          data:{
            cid:id
          },
          success:res2=>{
            //获取一篇文章的id,根据文章的id找到该文章下的评论
            let id=res2.data[0].id;
            uni.request({
              url:api,
              data:{
                aid:id
              },
              success:res3=>{
                //找到该文章下所有的评论
              }
            })
          }
        })
      }
    })
  }-->
<!-- 回调地狱1.0解决版本 -->
<!-- 用callback回调函数来解决，就是封装，然后用函数回调  -->
<!-- this.getNav(res=>{
      let id = res.data[0].id;
      this.getList(id，res=>{
        let id = res.data[0].id;
        .....
      })
    }) -->
<!-- 具体逻辑就是，getNav是封装后的函数，这里传入一个函数作为形参，然后执行getNac的时候，拿到数据，把数据传递给形参，形参拿到数据后开始执行自己的代码，只不过这里形参的代码写在了上面 -->
<!-- 回调地狱 2.0解决版本Promise-->
<!-- promise有三种状态 ：pending，resolve、reject-->
<!-- let p = new Promise((resolve,reject)=>{----这里的resolve和reject的位置是不能换的，第一个对应的是成功，第二个对应的是失败
    uni.request({
      url:api.
      success:res=>{---success是什么， 是 uni.request 网络请求 API 里的固定配置项，服务器执行成功后会把数据封装成一个对象，作为参数传给success回调
        resolve(res);
      },
      fail:err=>{
        reject(err)
      }
    })
  }) 
  p.then(res=>{...}).catch(err=>{...})-->
<!-- 进一步简化 -->
<!-- uni.showLoading({
  title:"数据加载中...."
}) 
let p1 = this.getNav();
let p2 = this.getList();
let p3 = this.getComment();
Promise.all([p1,p2,p3]).then(res=>{
  uni.hideLoading()
})-->
<!-- 用async和await进行异步同步化 -->
<!-- async/await 是 Promise 的「语法糖」—— 它没有创造新功能，只是把 Promise 的链式写法（.then().then()），包装成了看起来像同步代码的样子，让异步代码更易读、更易维护！ -->
<!-- async：标记函数为「异步函数」
作用：放在函数前面，告诉 JS：“这个函数里有异步操作，它会返回一个 Promise”。 -->
<!-- await：「等待」Promise 的结果 -->
<!-- 作用：只能用在 async 函数里，它会暂停当前 async 函数的执行，直到后面的 Promise 状态变成 fulfilled（成功），然后把 Promise 的结果返回给左边的变量。 -->
<!-- 注意事项
 await 只能在 async 函数里用：不能在普通函数或全局作用域直接用 await（除非是「顶层 await」，但新手阶段先记住这个规则）。
 async 函数返回的是 Promise：所以调用 async 函数后，依然可以用 .then() 接收结果，或者用 await 再等它。
 await 后面如果不是 Promise：会自动转成 Promise.resolve(值)，比如 await 1 相当于 await Promise.resolve(1)。-->
<template>
  <view>

  </view>
</template>

<script setup>

</script>

<style lang="scss">

</style>