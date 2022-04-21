<template>
  <view class="container">
    <text class="text-4xl text-neutral-600">{{ greeting }}</text>
  </view>
</template>

<script setup>
  import { ref } from 'vue';
  const greeting = ref('hello');
</script>

<style></style>
