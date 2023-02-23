<template>
	<view>

		<view class="searchView">
			<div class="searchBox">
				<input v-model="input" placeholder="请输入你要查的歌曲">
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

</style>
