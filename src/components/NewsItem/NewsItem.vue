<template>
  <text class="block">{{ news.title }}</text>
  <view
    v-if="news.thumbnail_pic_s02 || news.thumbnail_pic_s03"
    class="flex my-2"
  >
    <image class="w-1/3 h-24 object-none" :src="news.thumbnail_pic_s" />
    <image
      class="w-1/3 h-24 object-none ml-[1px]"
      v-if="news.thumbnail_pic_s02"
      :src="news?.thumbnail_pic_s02"
    />
    <image
      class="w-1/3 h-24 object-none ml-[1px]"
      v-if="news.thumbnail_pic_s03"
      :src="news?.thumbnail_pic_s03"
    />
  </view>
  <image
    class="my-2 object-none h-44 w-full"
    v-else-if="
      news.thumbnail_pic_s && !news.thumbnail_pic_s02 && !news.thumbnail_pic_s03
    "
    :src="news.thumbnail_pic_s"
  />
  <view class="flex text-xs text-neutral-500"
    ><text>{{ news.author_name }}</text>
    <text class="ml-2">{{ date }}</text></view
  >
</template>

<script setup>
  import dayjs from 'dayjs';
  import 'dayjs/locale/zh-cn';
  import relativeTime from 'dayjs/plugin/relativeTime';
  dayjs.extend(relativeTime);

  dayjs.locale('zh-cn');

  const props = defineProps({
    news: Object,
  });

  const date = dayjs(props.news.date).fromNow(true) + '前';
</script>

<style lang="scss" scoped></style>
