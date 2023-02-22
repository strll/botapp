<template>
	<view>
		<view class="myimg">
			<image :src="newstitle.url"></image>
		</view>
		<view v-text="newstitle.msg" class="mytext"></view>


		<view v-for="objs in list">
			<view v-text="objs.title" class="mytext"></view>
			<view v-for=" obj in objs.img" class="myimg">
				<image :src="obj"></image>
			</view>


		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				newstitle: {
					msg: "",
					url: ""
				},
				list: []

			}
		},
		onLoad() {
			this.getmsg()
		},
		methods: {
			filtersFnc(arr) {
				// console.log(arr)
				let list = []
				let newArr = JSON.parse(JSON.stringify(arr))
				this.newstitle.url = arr[0]
				this.newstitle.msg = arr[1] + "\n" + arr[2]
				newArr.splice(0, 3)

				for (let index = 0; index < newArr.length; index++) {
					const element = newArr[index];
					if (element.indexOf('http') == 0) {
						list[list.length - 1].img.push(element)
					} else {
						list.push({
							title: element,
							img: []
						})
					}
				}
				this.list = list
			},














			getmsg() {
				uni.request({
					url: "http://150.158.77.254:9991/bot/GetNews",
					success: ref => {

						this.filtersFnc(ref.data.data);
						console.log(this.list)
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
	.myimg {
		display: flex;

		justify-content: center;

		align-items: center;
	}

	,
	.mytext {


		text-indent: 2em;
		font-family: "微软雅黑";
		font-size: 30rpx;
		line-height: 26px;
		line-height: 35rpx;
	}
</style>
