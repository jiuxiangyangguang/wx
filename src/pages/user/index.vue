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
import { onMounted, ref } from 'vue'
const title = ref('Hello')
const arr = ref<string[]>([])

onMounted(async () => {
  // const tuya = new TuyaContext({
  //   baseUrl: 'https://openapi.tuyacn.com',
  //   accessKey: '89km4dqa4vncmweshvex',
  //   secretKey: '6ddaa9d15cde45e79c8136ef52b7c81e'
  // })

  // const device = await tuya.device.detail({
  //   device_id: 'vdevo170859366267271'
  // })
  uni.request({
    url: 'https://openapi.tuyacn.com/v1.0/iot-03/devices/vdevo170859366267271/status', // 你的 API 地址
    method: 'GET',
    header: {
      sign_method: 'HMAC-SHA256',
      client_id: '89km4dqa4vncmweshvex',
      t: '1708595094175',
      mode: 'cors',
      'Content-Type': 'application/json',
      sign: '3766A09D8CBA92BE619320B02B908ED4FF492720EF10A12EFE09BABD7E6C2544',
      access_token: '7800b6533fd4c06b0268db650d877086'
    },
    success: (res) => {
      arr.value = res.data as string[]
    },
    fail: (err) => {
      console.error(err)
    }
  })
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
<!-- curl --request GET "https://openapi.tuyacn.com/v1.0/iot-03/devices/vdevo170859366267271/status" --header "sign_method: HMAC-SHA256" --header "client_id: 89km4dqa4vncmweshvex" --header "t: 1708594358091" --header "mode: cors" --header "Content-Type: application/json" --header "sign: FC977FDDF7C23B0377192ABCB686F42DB01BA94F2126879804A97327A3BBAB23" --header "access_token: 7800b6533fd4c06b0268db650d877086" -->
