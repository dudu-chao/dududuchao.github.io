<template>
  <view class="blockly-page">
    <web-view src="{{ webUrl }}" bindmessage="onWebMessage" bindload="onWebLoad" />
  </view>
</template>

<script>
export default {
  data() {
    return {
      // 设置为实际部署的Blockly网页URL
      webUrl: 'https://yourdomain.com/blockly-page.html'
    }
  },
  methods: {
    onWebLoad(e) {
      console.log('Blockly编辑器网页加载成功');
    },
    onWebMessage(e) {
      const code = e.detail.data[0]; // 来自网页的消息数据
      console.log('接收到 Blockly 生成的代码:', code);
      // 可以将代码保存到本地或显示出来
      uni.setStorage({
        key: 'latestCode',
        data: code
      });
      uni.showModal({
        title: '代码已生成',
        content: code,
        showCancel: false
      });
    }
  }
}
</script>

<style>
.blockly-page {
  width: 100%;
  height: 100%;
}
</style>
