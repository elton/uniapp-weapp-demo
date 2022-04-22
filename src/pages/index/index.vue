<template>
  <view class="container m-4 space-y-5">
    <view
      v-for="news in newsList"
      :key="news.uniquekey"
      class="text-neutral-700"
    >
      <!-- UniApp中， 在components目录下的组件会自动导入 -->
      <NewsItem :news="news" />
    </view>
  </view>
</template>

<script setup>
  import { ref, reactive } from 'vue';
  import { onLoad, onPullDownRefresh, onReachBottom } from '@dcloudio/uni-app';

  const newsList = reactive([]);
  const page = ref(1);
  const loadDate = (n) => {
    console.log('current page: ', n);
    uni.showLoading({
      title: '加载中',
    });
    uni.request({
      url: `https://v.juhe.cn/toutiao/index?page=${n}&page_size=10&key=e7eb489fc2dd2a193e3c40b1b2f581e6`,
      success: (res) => {
        // console.log(res.data.result.data);
        newsList.push(...res.data.result.data);
        uni.hideLoading();
        console.log(newsList);
      },
    });
  };
  onLoad(() => {
    loadDate(page.value);
  });

  onPullDownRefresh(() => {
    // 清空原有数据
    newsList.length = 0;
    page.value = 1;
    loadDate(page.value);
    console.log('refresh');
    setTimeout(() => {
      uni.stopPullDownRefresh();
    }, 1000);
  });

  onReachBottom(() => {
    page.value++;
    // console.log(page.value);
    loadDate(page.value);
    console.log('reach bottom');
  });
</script>

<style></style>
