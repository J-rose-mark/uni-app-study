<!--  box-shadow: 0 10rpx 20rpx rgba(0, 0, 0, 0.08); -->
<!-- box-shadow: 水平偏移 垂直偏移 模糊半径 阴影颜色 -->
<!-- 水平偏移正数向右偏移，垂直偏移正数向下偏移 -->
<!-- rgb代表颜色，然后最后一个是透明度，0-1，0是完全透明 -->
<!-- overflow：当子元素 / 内容的大小，超过了父容器的宽高限制时，把超出容器的部分直接隐藏，不显示在页面上。 -->
<!--   <image lazy-load :src="item.url" mode="widthFix" @click="onPreview(index)"></image>
        lazy-load懒加载，没有一下子加载全部资源，能节约资源
         uni.previewImage：预览图片-->
<!-- 刷新有两种方法
 第一种定义函数：onPullDownRefresh,需要将之前的数据归零
 第二种uni自带的uni.startPullDownRefresh(OBJECT)-->

<!-- 菜单--由分段选择器实现
 <uni-segmented-control :current="current" :values="values" @clickItem="onClickItem" styleType="button"
   activeColor="#4cd964"></uni-segmented-control>
  自带下标-->
<template>
  <view class="container">
    <view class="menu">
      <uni-segmented-control :current="current" :values="values" @clickItem="onClickItem" styleType="button"
        activeColor="#4cd964"></uni-segmented-control>
    </view>
    <view class="layout">
      <view class="box" v-for="(item,index) in pets" :key="item._id">
        <view class="pic">
          <image lazy-load :src="item.url" mode="widthFix" @click="onPreview(index)"></image>
        </view>
        <view class="text">{{item.content}}</view>
        <view class="author">——{{item.author}}</view>
      </view>
    </view>
    <view class="float">
      <view class="item" @click="onRefresh">
        <uni-icons type="refresh-filled" size="30"></uni-icons>
      </view>
      <view class="item" @click="onTop">
        <uni-icons type="arrow-up" size="30"></uni-icons>
      </view>
      <view class="loadmore">
        <uni-load-more status="more"></uni-load-more>
      </view>
    </view>
  </view>
</template>

<script setup>
  import {
    computed,
    ref
  } from 'vue';
  import {
    onReachBottom,
    onPullDownRefresh
  } from '@dcloudio/uni-app'
  const pets = ref([]);
  //网络请求，加载图片
  function network() {
    uni.showLoading()
    uni.request({
      url: "https://tea.qingnian8.com/tools/petShow",
      data: {
        size: 2,
        type: classify[current.value].key
      },
      header: {
        "access-key": "966788"
      },
    }).then(res => {
      if (res.data.errCode === 0) {
        pets.value = [...pets.value, ...res.data.data]
      } else if (res.data.errCode === 400) {
        uni.showToast({
          title: res.data.errMsg,
          icon: "none"
        })
      }
    }).catch(err => {
      uni,
      showToast({
        title: "请求有误，请重新刷新",
        icon: "none"
      })
    }).finally(() => {
      uni.hideLoading(),
        uni.stopPullDownRefresh()
    })
  }

  //触底刷新
  onReachBottom(() => {
    network()
  });
  // 下拉刷新
  onPullDownRefresh(() => {
    pets.value = [],
      network()
  })
  // 点击刷新
  const onRefresh =
    function() {
      uni.startPullDownRefresh();
    }
  const onTop = function() {
    uni.pageScrollTo({
      scrollTop: 0,
      duration: 100
    })
  }


  // 预览图片
  const onPreview = function(index) {
    let urls = pets.value.map(item => item.url)
    uni.previewImage({
      current: index,
      urls
    })
  }
  //点击菜单
  /* 点击后可以切换种类，因此需要传递狗和猫的分类数据，这个需要在网络请求中传入种类；
   创建数组，猫和狗的字样，并且应该带一个索引的值key，
   数组的小标对应的key，因此点击那个数组的时候，顺带把key传进网络请求里*/
  const current = ref(0)
  const classify = [{
      key: "all",
      value: "全部"
    }, {
      key: "dog",
      value: "狗"
    },
    {
      key: "cat",
      value: "猫"
    }
  ]
  network();
  const values = computed(() => classify.map(item => item.value))
  const onClickItem = (e) => {
    current.value = e.currentIndex
    pets.value = [],
      network()
  }
</script>

<style lang="scss">
  // 全局变量
  :root {
    --primary-color: #3498db;
    --secondary-color: #2ecc71;
    --text-primary: #333;
    --text-secondary: #666;
    --text-light: #999;
    --background: #f5f7fa;
    --card-bg: #ffffff;
    --shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
    --shadow-hover: 0 12rpx 32rpx rgba(0, 0, 0, 0.12);
    --border-radius: 20rpx;
    --transition: all 0.3s ease;
  }

  .container {
    background-color: var(--background);
    min-height: 100vh;

    .menu {
      padding: 20rpx 30rpx 0;
      background-color: var(--card-bg);
      position: sticky;
      top: 0;
      z-index: 10;
      box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
    }

    .layout {
      padding: 30rpx;

      .box {
        margin-bottom: 40rpx;
        background-color: var(--card-bg);
        border-radius: var(--border-radius);
        overflow: hidden;
        box-shadow: var(--shadow);
        transition: var(--transition);
        transform: translateY(0);

        &:hover {
          box-shadow: var(--shadow-hover);
          transform: translateY(-4rpx);
        }

        .pic {
          position: relative;
          overflow: hidden;

          image {
            width: 100%;
            height: 300rpx;
            object-fit: cover;
            transition: var(--transition);

            &:hover {
              transform: scale(1.05);
            }
          }
        }

        .text {
          padding: 30rpx 30rpx 15rpx;
          color: var(--text-primary);
          font-size: 34rpx;
          line-height: 1.5;
          font-weight: 500;
        }

        .author {
          padding: 0 30rpx 30rpx;
          text-align: right;
          color: var(--text-light);
          font-size: 26rpx;
          font-style: italic;
        }
      }
    }

    .float {
      position: fixed;
      right: 30rpx;
      bottom: 100rpx;
      padding-bottom: env(safe-area-inset-bottom);
      display: flex;
      flex-direction: column;
      gap: 20rpx;

      .item {
        width: 80rpx;
        height: 80rpx;
        background-color: var(--card-bg);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: var(--shadow);
        border: none;
        transition: var(--transition);

        &:hover {
          background-color: var(--primary-color);
          color: white;
          box-shadow: var(--shadow-hover);
          transform: scale(1.1);
        }
      }

      .loadmore {
        margin-top: 10rpx;
      }
    }
  }

  // 分段选择器样式覆盖
  :deep(.uni-segmented-control) {
    border-radius: 12rpx;
    overflow: hidden;

    .uni-segmented-control__item {
      font-size: 32rpx;
      height: 80rpx;
    }

    .uni-segmented-control__item--active {
      background-color: var(--primary-color) !important;
      color: white !important;
    }
  }

  // 加载更多样式
  :deep(.uni-load-more) {
    margin: 40rpx 0;
  }

  // 图标样式
  :deep(.uni-icons) {
    transition: var(--transition);
  }

  // 响应式设计
  @media (max-width: 375px) {
    .container {
      .layout {
        padding: 20rpx;

        .box {
          margin-bottom: 30rpx;

          .pic image {
            height: 250rpx;
          }

          .text {
            font-size: 32rpx;
            padding: 25rpx 25rpx 10rpx;
          }

          .author {
            font-size: 24rpx;
            padding: 0 25rpx 25rpx;
          }
        }
      }

      .float {
        right: 20rpx;
        bottom: 80rpx;

        .item {
          width: 70rpx;
          height: 70rpx;
        }
      }
    }
  }
</style>