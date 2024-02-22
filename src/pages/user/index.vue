<template>
  <view class="content">
    <image class="logo" src="/static/logo.png" />
    <view class="text-area">
      <text class="title">第一个小程序</text>
    </view>
    <view v-for="item in arr" :key="item" class="title">{{ item }}</view>
  </view>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
const title = ref('Hello')
const arr = ref<string[]>([])

onMounted(() => { 

  uni.request({
    url: 'http://192.168.6.97:3000', // 你的 API 地址
    method: 'GET',
    success: (res) => {
    arr.value = res.data as string[]
    },
    fail: (err) => {
      console.error(err);
    }
  });
})
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin-top: 200rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}

.text-area {
  display: flex;
  justify-content: center;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}
</style>
