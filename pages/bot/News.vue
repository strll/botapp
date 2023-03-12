<template>
	<view class="newsBox">
		<view class="myimg">
			<image :src="newstitle.url"></image>
		</view>
		<view v-text="newstitle.msg" class="mytext"></view>
		<view class="listBox">
			<view v-for="objs in list" class="listItem">
				<!-- 	<view v-text="objs.title" class="mytext"></view> -->
				<u--text prefixIcon="zhihu" iconStyle="font-size: 19px" :text="objs.title"></u--text>
				<view v-for=" obj in objs.img" class="myimg itemImg">
					<u--image :showLoading="true" :src="obj"></u--image>
				</view>
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

<style lang="scss">
	.myimg {
		display: flex;

		justify-content: center;

		align-items: center;
	}

	.mytext {

		font-weight: bold;
		padding: 0 10rpx;
		margin: 10rpx 0;
		text-indent: 2em;
		font-family: "微软雅黑";
		font-size: 30rpx;
		line-height: 26px;
		line-height: 35rpx;
	}
	
	.newsBox{
		background-color: white;
	}
	
	.listBox{
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		.listItem{
			width: 90%;
			padding: 10rpx 15rpx 20rpx;
			margin-bottom: 20rpx;
			background-color: $uni-bg-color-grey;
			border-radius: 10rpx;
			.itemImg{
				margin-top: 20rpx;
			}
		}
	}
</style>
