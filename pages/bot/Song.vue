<template>
	<view>

		<view class="searchView">
			<div class="searchBox">
				<input v-model="input" placeholder="请输入你要查的歌曲"></input>
				<button type="primary" @click="get()">查询</button>
			</div>
		</view>
		<main>

		</main>

		<view>
			<view v-text="songer" class="center"></view>

			<image :src="pic" class="center"></image>
		</view>
		<view class="center">

			<embed :src="msg">
		</view>


	</view>
</template>

<script>
	export default {
		onLoad() {

		},

		data() {
			return {
				songer: "",
				pic: "",
				input: "",
				msg: ""
			}
		},
		methods: {

			get() {
				uni.request({
					url: "http://150.158.77.254:9991/bot/GetSong?song=" + this.input,
					success: ref => {
						console.log(ref.data.data.data),
							this.msg = ref.data.data.data.url,
							this.pic = ref.data.data.data.cover,
							console.log(this.pic),
							this.songer = ref.data.data.data.singer
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
	.searchView {
		margin: 1em 0;
		width: 100%;
		display: flex;
		justify-content: center;

		.searchBox {
			width: 90%;
			display: flex;
			align-items: center;

			input {
				height: 3em;
				width: 70%;
				border: 2px solid #c4c7ce;
				border-radius: 10rpx 0 0 10rpx;
				background-color: #f1f1f1;
				padding-left: 1em;
			}

			button {
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

	main {
		padding: 0 5%;
		font-size: 14px;
	}

	.center {
		display: flex;
		justify-content: center;
	}
</style>
