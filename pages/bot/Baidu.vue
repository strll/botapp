<template>
	<view>
		<view class="searchView">
			<div class="searchBox">
				<input v-model="input" placeholder="请输入内容"></input>
				<button type="primary" @click="get()">查询</button>
			</div>
		</view>
		<main>
			{{msg}}
		</main>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				input: "",
				msg: ""
			}
		},
		methods: {
			get() {
				uni.request({
					url: "http://150.158.77.254:9991/bot/GetBaidu?msg=" + this.input,
					success: ref => {
						this.msg = ref.data.data.msg
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

<style lang="scss">
	.searchView{
		margin: 1em 0;
		width: 100%;
		display: flex;
		justify-content: center;
		.searchBox{
			width: 90%;
			display: flex;
			align-items: center;
			input{
				height: 3em;
				width: 70%;
				border: 2px solid #c4c7ce;
				border-radius: 10rpx 0 0 10rpx;
				background-color: #f1f1f1;
				padding-left: 1em;
			}
			button{
				height: 100%;
				width: 30%;
				display: flex;
				overflow: hidden;
				align-items: center;
				justify-content: center;
				border-radius: 0 10rpx 10rpx 0;
			}
		}
	}
	main{
		padding: 0 5%;
		font-size: 14px;
	}
	
</style>
