<template>
	<view>


		<!--
		                "\n 4.nana图片 发送随机二次元图片(2022.8.1新增) " +
		                "\n 如果机器人出现bug请管理员及时禁言 " +
		                "\n 8.nana天气 新增天气查询(2022.8.15)" +
		                "\n 9.nana模块管理" +
		                "\n 10.nana点歌(示例:nana点歌Hurt)" +
		                "\n 11.nana每日新闻" +
		                "\n 12.nana微博热搜" +
		                "\n 13.nana历史上的今天"
		                + "\n 15.nana翻译(示例: nana翻译 hello)"
		                + "\n 16.nana百度(使用方法示例: nana百度 春节) "
		                + "\n 17.nana查询 使用方法同上(改接口失效请使用百度功能进行搜索)"
		                + "\n 18.nana摸鱼日历" +
		                "\n 19.nana找番(用法: nana找番+动漫截图)"
		                + "\n 20.nana聊天(nana监听你发送的信息并且做出回复 退出请输入nana退出聊天)"
		                + "\n 21.nana今天吃什么(或者使用 饿了) 随机发送\n"
		                + "\n 22.nana动漫资讯"
		                + "\n 23.nana小鸡词典 (示例: nana小鸡词典 盐系) 微博恶意盗取小鸡词典文库 小鸡词典在于微博的官司中入不敷出 现网站服务器因为某些特殊原因永久关闭 "
		               
		                "\n 26.nana搜图 (2023.2.9新增)" -->
		<ul>
			<li><img src="static/logo.png">
				<div><button @click="AccountInfo()">进入聊天页面</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="CartoonNews()">进入动漫新闻页面</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="Eattoday()">随机roll一个食物吧</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="Baidu()">去查一查你不明白的东西吧</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="HistoryTody()">历史上的今天发生了什么</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="News()">今天发生了什么</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="NowWeather()">今天天气怎么样</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="Translation()">翻译</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="Song()">搜歌</button></div>
			</li>
			<li><img src="static/logo.png">
				<div><button @click="WbTop10()">微博热搜</button></div>
			</li>
		</ul>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},

		onBackPress(event) {

			uni.showModal({
				title: '提示',
				content: '你是否要登出当前帐号',
				success: function(res) {
					if (res.confirm) {
						uni.setStorageSync("login", false);
						uni.navigateTo({
							url: "/pages/index/index"
						})

					} else if (res.cancel) {

					}
				}
			});




			return true;
		},

		methods: {

			WbTop10() {
				uni.navigateTo({
					url: "/pages/bot/WbTop10"
				})
			},
			Song() {
				uni.navigateTo({
					url: "/pages/bot/Song"
				})
			},
			Translation() {
				uni.navigateTo({
					url: "/pages/bot/Translation"
				})
			},
			NowWeather() {
				uni.navigateTo({
					url: "/pages/bot/NowWeather"
				})
			},
			News() {
				uni.navigateTo({
					url: "/pages/bot/News"
				})
			},
			HistoryTody() {
				uni.navigateTo({
					url: "/pages/bot/HistoryTody"
				})
			},
			Baidu() {
				uni.navigateTo({
					url: "/pages/bot/Baidu"
				})
			},
			Eattoday() {
				uni.navigateTo({
					url: "/pages/bot/Eattoday"
				})
			},
			CartoonNews() {
				uni.navigateTo({
					url: "/pages/bot/CartoonNews"
				})
			},
			AccountInfo() {
				uni.navigateTo({
					url: "/pages/bot/AccountInfo"
				})
			},


		}
	}
</script>

<style lang="scss">
	view {

		// height: 1900px;
		// background-color: pink;
		ul {
			list-style: none;
			padding: 0;
			display: flex;
			flex-direction: column;

			li {
				height: 4em;
				padding: 0.4em;
				display: flex;

				img {
					display: none;
					// display: inline-block;
					//反转注释状态，显示图片icon
					height: 4em;
					width: 4em;
				}

				div {
					// width: calc( 100% - 4em);
					width: 100%;
					//反转注释状态，为图片icon留出空间   
					display: inline-block;

					button {
						display: flex;
						height: 100%;
						align-items: center;
					}
				}
			}
		}
	}
</style>
