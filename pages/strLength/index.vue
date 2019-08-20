<template>
  <view>
    <textarea v-model="inputStr" class="input-area"></textarea>
    <view class="btn-area">
    	<button type="primary" size="mini" class="img2base64" @click="jsClick">计算输入字符串长度</button>
    </view>
    <view class="js-result">
      <text class="js-text">{{inputStrLen}}</text>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        inputStr: '',
        inputStrLen: ''
      }
    },
    methods: {
      jsClick() {
        this.inputStrLen = this.inputStr.trim().length
      }
    }
  }
</script>

<style lang="scss">
  .input-area {
    width: 500rpx;
    height: 250rpx;
    border: 2rpx #C8C7CC dashed;
    margin: 10rpx auto;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5rpx;
  }
  .btn-area {
  	padding: 10rpx 0rpx;
  	text-align: center;
  }
  .js-result {
    width: 500rpx;
    border: 2rpx #C8C7CC dashed;
    margin: 10rpx auto;
    border-radius: 8rpx;
    .js-text {
      padding: 10rpx 5rpx;
    }
  }
</style>
