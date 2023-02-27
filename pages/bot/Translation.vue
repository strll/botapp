<template>
	<view>
		<view class="searchView">
			<div class="searchBox">
				<input v-model="msg" placeholder="请输入查询的单词" @confirm="getmsg">
				<button type="primary" @click="getmsg()">查询</button>
			</div>
		</view>
		<main v-html="remsg">

		</main>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				remsg: "",
				msg: ""
			}
		},
		methods: {
			getmsg() {
				uni.request({
					url: "http://150.158.77.254:9991/bot/GetTranslation?msg=" + this.msg,
					success: ref => {
						this.remsg = ref.data.data
            this.remsg=this.remsg.replaceAll("\n","<br>")
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
