<template>
  <view class="container m-4">
    <view>
      <text class="text-lg">{{ newsDetail?.data?.detail?.title }}</text>
    </view>
    <view class="flex justify-between text-sm text-neutral-500 my-2">
      <text>{{ newsDetail?.data?.detail?.author_name }}</text>
      <text>{{
        dayjs(newsDetail?.data?.detail?.date).fromNow(true) + '前'
      }}</text>
    </view>
    <view class="text-neutral-600 pb-6">
      <rich-text :nodes="content?.data"></rich-text>
    </view>
  </view>
</template>

<script setup>
  import { onLoad } from '@dcloudio/uni-app';
  import { ref, reactive } from 'vue';
  import dayjs from 'dayjs';
  import 'dayjs/locale/zh-cn';
  import relativeTime from 'dayjs/plugin/relativeTime';
  dayjs.extend(relativeTime);

  dayjs.locale('zh-cn');

  const newsDetail = reactive({ data: {} });
  const content = ref({ data: '' });

  const getNewsDetail = (newsID) => {
    uni.showLoading({
      title: '加载中',
    });
    uni.request({
      url: `https://v.juhe.cn/toutiao/content?uniquekey=${newsID}&key=e7eb489fc2dd2a193e3c40b1b2f581e6`,
      success: (res) => {
        // console.log(res.data.result.content);
        newsDetail.data = res.data.result;
        // 设置正文样式
        content.value = {
          data: res.data.result.content
            .replace(/\<img/gi, '<img style="margin: 0.5em 0"')
            .replace(/\<p/gi, '<p style="margin: 0.75em 0"'),
        };
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
