<template>
  <text class="block">{{ news.title }}</text>
  <image
    class="block mx-auto my-2"
    v-if="news.thumbnail_pic_s"
    :src="news.thumbnail_pic_s"
  />
  <view class="flex justify-between text-sm text-neutral-500"
    ><text>{{ news.author_name }}</text> <text>{{ date }}</text></view
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
