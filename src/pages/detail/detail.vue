<template>
  <view class="container m-4">
    <view>
      <text class="text-lg">{{ newsDetail?.data?.detail?.title }}</text>
    </view>
    <view class="flex justify-between text-sm text-neutral-500 my-2">
      <text>{{ newsDetail?.data?.detail?.author_name }}</text>
      <text>{{ newsDetail?.data?.detail?.date }}</text>
    </view>
    <view class="text-neutral-600">
      <rich-text :nodes="newsDetail?.data?.content"></rich-text>
    </view>
  </view>
</template>

<script setup>
  import { onLoad } from '@dcloudio/uni-app';
  import { reactive } from 'vue';

  const newsDetail = reactive({ data: {} });

  const getNewsDetail = (newsID) => {
    uni.showLoading({
      title: '加载中',
    });
    uni.request({
      url: `https://v.juhe.cn/toutiao/content?uniquekey=${newsID}&key=e7eb489fc2dd2a193e3c40b1b2f581e6`,
      success: (res) => {
        // console.log(res.data.result);
        newsDetail.data = res.data.result;
        uni.hideLoading();
        // console.log(newsDetail.data);
      },
    });
  };

  onLoad((option) => {
    // console.log('detail onLoad, newsID: ', option.newsID);

    getNewsDetail(option.newsID);
  });
</script>

<style scoped>
  page p {
    margin-bottom: 1.5rem;
  }
</style>
