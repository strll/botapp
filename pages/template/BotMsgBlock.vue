<template>
  <view class="flex-row-start margin-left margin-top one-show msgBlock">
    <view class="chat-img flex-row-center" v-bind:class="{'picHidden':!x.firstMsg}">
      <!-- <image style="height: 75rpx;width: 75rpx;" src="../../static/nana.jpg" mode="aspectFit"></image> -->
    </view>
    <view class="flex" style="width: 500rpx;">
      <view class="margin-left padding-chat flex-column-start"
            style="border-radius: 35rpx;background-color: #f9f9f9;">
        <text style="word-break: break-all;">{{ x.msg }}</text>
        <!-- 消息模板 =>初次问候 -->
        <!-- <view class="flex-column-start" v-if="x.type==1" style="color: #2fa39b;">
          <text style="color: #838383;font-size: 22rpx;margin-top: 15rpx;">你可以这样问我:</text>
          <text @click="answer(index)" style="margin-top: 30rpx;"
            v-for="(item,index) in x.questionList" :key="index">{{item}}</text>
          <view class="flex-row-start  padding-top-sm">
            <text class="my-neirong-sm">没有你要的答案?</text>
            <text class="padding-left" style="color: #007AFF;">换一批</text>
          </view>
        </view> -->
        <!-- 消息模板 =>多个答案 -->
        <view class="flex-column-start" v-if="x.type==2" style="color: #2fa39b;">
          <text style="color: #838383;font-size: 22rpx;margin-top: 15rpx;">猜你想问:</text>
          <!-- 连接服务器应该用item.id -->
          <text @click="answer" style="margin-top: 30rpx;"
                v-for="(item,index) in x.questionList" :key="index">{{ item }}
          </text>
        </view>
        <view class="margin-left padding-chat flex-column-start imageMsg"
              style="border-radius: 35rpx;background-color: #f9f9f9;" v-if="urlCheck(x.url)">
          <img v-if="urlCheck(x.url)" v-bind:src="x.url" alt="图片">
        </view>
        <!-- 消息模板 => 无法回答-->
        <!-- <view class="flex-column-start" v-if="x.type==0">
          <text class="padding-top-sm" style="color: #2fa39b;">提交意见与反馈</text>
          <text
            style="color: #838383;font-size: 22rpx;margin-top: 15rpx;">下面是一些常见问题,您可以点击对应的文字快速获取答案:</text>
          <text @click="answer(index)" style="margin-top: 30rpx;color: #2fa39b;"
            v-for="(item,index) in x.questionList" :key="index">{{item}}</text>
          <view class="flex-row-start  padding-top-sm">
            <text class="my-neirong-sm">没有你要的答案?</text>
            <text class="padding-left" style="color: #1396c5;">换一批</text>
          </view>
        </view> -->


      </view>
    </view>
  </view>
</template>
<script>
export default {
  name: 'botMsgBlock',
  props: {
    answer: {},
    x: {}
  },
  methods:{
    urlCheck(obj){
      if (typeof(obj) == "undefined")
        return false;
      if (!obj && typeof(obj)!="undefined" && obj!==0)
        return false;
      return obj.length !== 0;
    }
  }
}
</script>
