<template>
  <view class="container m-4 space-y-5">
    <view v-for="news in newsList" class="text-neutral-700">
      <text class="block">{{ news.title }}</text>
      <image
        class="block mx-auto my-2"
        v-if="news.thumbnail_pic_s"
        :src="news.thumbnail_pic_s"
      />
      <view class="flex justify-between text-sm text-neutral-500"
        ><text>{{ news.author_name }}</text> <text>{{ news.date }}</text></view
      >
    </view>
  </view>
</template>

<script setup>
  import { reactive } from 'vue';
  import { onLoad } from '@dcloudio/uni-app';

  const newsList = reactive([]);
  onLoad(() => {
    uni.request({
      url: 'http://v.juhe.cn/toutiao/index?type=top&page_size=10&key=e7eb489fc2dd2a193e3c40b1b2f581e6',
      success: (res) => {
        // console.log(res.data.result.data);
        newsList.push(...res.data.result.data);
        console.log(newsList);
      },
    });
  });
</script>

<style></style>
