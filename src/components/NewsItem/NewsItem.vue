<template>
  <text class="block">{{ news.title }}</text>
  <image
    class="block mx-auto my-2"
    v-if="news.thumbnail_pic_s"
    :src="news.thumbnail_pic_s"
  />
  <view class="flex justify-between text-sm text-neutral-500"
    ><text>{{ news.author_name }}</text> <text>{{ news.date }}</text></view
  >
</template>

<script setup>
  const props = defineProps({
    news: Object,
  });
</script>

<style lang="scss" scoped></style>
