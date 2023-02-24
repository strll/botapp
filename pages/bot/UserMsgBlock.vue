<template>
  <view v-if="x.my" class="flex justify-end padding-right one-show  align-start  padding-top">
    <!-- 	<image v-if="!x.my" class="chat-img" src="../../static/..." mode="aspectFill" ></image> -->
    <view class="flex justify-end" style="width: 400rpx;">
      <view class="margin-left padding-chat bg-cyan" style="border-radius: 35rpx;">
        <text style="word-break: break-all;">{{ x.msg }}</text>
      </view>
    </view>
    <!-- <image class="chat-img margin-left" src="../../static/..." mode="aspectFill" ></image> -->
  </view>
</template>
<script>
export default {
  name: 'userMsgBlock',
  props: {
    x: {}
  }
}
</script>