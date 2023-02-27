<template>
	<view class="eatTodayBox">
		<div class="center">
			<button type="primary" @click="get()">Roll!</button>
		</div>
		<view v-text="showmsg"></view>

		<img :src="myurl" :alt="msg">

	</view>
</template>

<script>
	export default {
		data() {
			return {
				showmsg: "",
				msg: "",
				qq: "",
				myurl: ""
			}
		},
		methods: {
			// "message": " 熟鸡肉",
			//        "qq": "†穆尔Moore†(2590892290)",
			//        "url": "http://43.142.125.197:9000/bot/2023/01/02/2b0fdf77d3ce42f1867669f299fc032f",
			async get() {
				this.msg = ""
					this.qq = ""
					this.myurl = ""
					this.showmsg = ""
				uni.request({
					url: "http://150.158.77.254:9991/bot/Eattoday",
					success: ref => {
						this.msg = ref.data.data.message
						this.qq = ref.data.data.qq,
							this.myurl = ref.data.data.url,
							this.showmsg = "要不试试" + ref.data.data.qq + "推荐的" + ref.data.data.message

					}
				})
			},

			onBackPress(event) {
				uni.navigateTo({
					url: "/pages/alltest/alltest"
				})
				return true;
			},
		}
	}
</script>

<style>
	.center {
		display: flex;
		justify-content: center;
	}
  .eatTodayBox{
    width: 90%;
    margin: 0 auto;
  }
  .eatTodayBox>*{
    margin-top: 10rpx;
  }
  .eatTodayBox>img{
    width: 100%;
  }
</style>
