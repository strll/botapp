<template>
	<view>
		<view class="searchView">
			<div class="searchBox">
				<input v-model="city" placeholder="请输入查询的城市" @confirm="getmsg">
				<button type="primary" @click="getmsg()">查询</button>
			</div>
		</view>
		<main v-html="msg">

		</main>
	</view>
</template>

<script>
export default {
	data() {
		return {
			city: "",
			msg: ""
		}
	},
	methods: {
		getmsg() {
			uni.request({
				url: "http://150.158.77.254:9991/bot/GetNowWeather?city=" + this.city,
				success: ref => {
					this.msg = ref.data.data
          this.msg=this.msg.replaceAll("\n","<br>")
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
</style>
