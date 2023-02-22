<template>
	<view>
		<view class="searchView">
			<div class="searchBox">
				<input v-model="input" placeholder="请输入内容">
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

<style>

</style>
