<template>

	<view class="login">
		<view class="top_item">
			<text style="color: #000000;font-size: 22px;font-weight: bold;">密码登录</text>

		</view>
		<view class="input-item" style="margin-top: 80rpx;">
			<view class="title-content">
				<text class="title">账号</text>
			</view>
			<input class="input" v-model="username" placeholder="请输入账号" style="margin-left: 40rpx;" />
		</view>
		<view class="input-item">
			<view class="title-content">
				<text class="title">密码</text>
			</view>
			<input class="input" v-model="password" placeholder="请输入密码" style="margin-left: 40rpx;" />

		</view>
		<view class="button" @click="login">登录</view>
		<u--text type="primary" text="注册" @click="gotoRegister()" align="right"></u--text>
		<u--text type="primary" text="忘记密码" @click="gotoChange_Password()" align="right"></u--text>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				username: "",
				password: "",
				title: 'Hello'
			}
		},
		onLoad() {
			this.go()
		},

		methods: {
			gotoRegister() {
				uni.navigateTo({
					url: '/pages/register/register'
				});
			},
			gotoChange_Password() {
				uni.navigateTo({
					url: '/pages/change_Password/change_Password'
				});
			},

			go() {

				if (uni.getStorageSync("login")) {
					uni.navigateTo({
						url: '/pages/alltest/alltest'
					});
				} else {
					uni.setStorageSync("login", false)
				};
			},
			async login() {
				uni.request({
					url: "http://150.158.77.254:9991/user/login?username=" + this.username + "&password=" +
						this
						.password,
					success: ref => {

						if (ref.data.data == true) {
							uni.setStorageSync("login", true)

							uni.navigateTo({
								url: '/pages/alltest/alltest'
							});
						} else {
							uni.setStorageSync("login", false)
							uni.showModal({
								showCancel: false,
								title: '提示',
								content: '您的密码错误',

							});


							this.password = ""
						}


					},
					fail() {

					}
				})
			},
		}
	}
</script>

<style>
	.top_item {
		display: flex;
		margin-top: 40rpx;
		margin-left: 32rpx;
		margin-right: 32rpx;
		justify-content: space-between;
	}

	.input-item {
		display: flex;
		margin-left: 32rpx;
		margin-right: 32rpx;
		height: 50px;
		align-items: center;
		border-bottom: 1px solid #efeff4;
		margin-bottom: 20rpx;

		.title-content {
			display: flex;
			justify-content: flex-start;
			align-items: center;

			.title {
				font-size: 18px;
			}
		}

		.input {
			flex: 1;
		}
	}

	.button {
		height: 50px;
		line-height: 50px;
		margin-top: 60rpx;
		margin-left: 32rpx;
		margin-right: 32rpx;
		border-radius: 50rpx;
		font-size: 20px;
		background-color: #008AFE;
		color: #FFFFFF;
		text-align: center;
	}
</style>
