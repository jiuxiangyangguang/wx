<template>
  <view class="content">
    <view class="text-area">
      <van-button @click="jump" type="primary">主页</van-button>
      <van-button @click="ca" type="primary">调用摄像头</van-button>
    </view>
  </view>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
const title = ref('Hello')

const jump = () => {
  uni.navigateTo({
    url: '/pages/detail/index'
  })
}

const ca = () => {
  uni.chooseMedia({
    count: 9,
    mediaType: ['image', 'video'],
    sourceType: ['album', 'camera'],
    maxDuration: 30,
    camera: 'back',
    success(res) {
      const files = res.tempFiles
      // files.forEach((file) => {
      //   console.log(file.path) // 这是文件的路径
      // })
    }
  })
}

onMounted(() => {})
</script>

<style></style>
