<template>
	<view>
		<view>
			<u--input placeholder="请输入要修改密码的用户名" border="surround" v-model="username" @change="change">

			</u--input>
		</view>
		<view>
			<u--input placeholder="请输入邮箱" border="surround" v-model="email"></u--input>
		</view>
		<view>
			<u--input placeholder="请输入验证码" border="surround" v-model="code"></u--input>
			<u-button type="primary" size="small" text="获取验证码" @click="getcode()"></u-button>

		</view>
		<view>
			<u--input placeholder=" 请输入密码" border="surround" v-model="password">
			</u--input>
			<u--input placeholder="请确认密码" border="surround" v-model="re_password"></u--input>
		</view>
		<u-button type="primary" size="small" text="注册帐号" @click="register()"></u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username: '',
				password: '',
				email: '',
				code: '',
				re_password: ''
			}
		},
		methods: {
			register() {
				const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
				if (this.username == '') {
					uni.showToast({
						icon: 'error',
						title: '未输入用户名',
						duration: 2000
					});
				} else if (this.password != this.re_password & this.password == '' & this.re_password == '') {
					uni.showToast({
						icon: 'error',
						title: '设定密码出错',
						duration: 2000
					});

				} else if (this.code == '') {
					uni.showToast({
						icon: 'error',
						title: '验证码不能位空',
						duration: 2000
					});
				} else if (!emailRegex.test(this.email)) {
					uni.showToast({
						icon: 'error',
						title: '邮箱格式出错',
						duration: 2000
					});
				} else {
					uni.request({
						url: "http://150.158.77.254:9991/user/resetpassword?username=" + this.username +
							"&password=" +
							this.password + "&email=" + this.email + "&code=" + this.code,

						success: ref => {
							console.log(ref)
							uni.showToast({
								icon: 'none',
								title: ref.data.data,
								duration: 2000
							});
							uni.navigateTo({
								url: '/pages/index/index'
							});
						}

					})
				}

			},

			getcode() {
				console.log(this.email)
				const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
				// 检查字符串是否匹配正则表达式
				if (this.email == '') {
					uni.showToast({
						icon: 'error',
						title: '请输入邮箱地址',
						duration: 2000
					});
				}

				if (!emailRegex.test(this.email)) {
					uni.showToast({
						icon: 'error',
						title: '请输入正确的邮箱地址',
						duration: 2000
					});
				} else {
					uni.request({
						url: "http://150.158.77.254:9991/user/resetpassword_code?email=" + this.email,
						success: ref => {
							uni.showToast({
								icon: 'success',
								title: '请查看你邮箱的验证码',
								duration: 2000
							});
						}
					})
				}
			},

			change(e) {}
		}
	}
</script>

<style lang="scss">

</style>
