<template>
	<view class="news-detail">
		<view class="title">{{info.title}}</view>
		<text class="time"
			:hidden="!info.con">{{'时间：'+info.add_time+'     浏览：'+info.view_num+'     文章来源：'+(info.remark||'网络')}}</text>
		<view class="con">
			<rich-text :nodes="info.con"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				info: {
					title: '今夜“大屠杀”！币圈崩盘无眠，50万人爆仓400亿，交易所紧急拔网线！国常会出手就知有没有，阿哈哈哈哈黑色系',
					add_time: '2021-09-08 11:09:08',
					view_num: 704,
					remark: '资金盘',
					con: '<div style="text-align:center;"><img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/d8590190-4f28-11eb-b680-7980c8a877b8.png"/></div>'
				}
			}
		},
		onLoad(options) {
			console.log(options)
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.news-detail {
		padding: 30rpx;
	}

	.news-detail .title {
		font-size: 36rpx;
		color: #000;
		line-height: 48rpx;
	}

	.news-detail .time {
		color: #9e9e9e;
		font-size: 24rpx;
		padding: 30rpx 0;
	}

	.news-detail .con {
		padding: 20rpx 0;
		font-size: 32rpx;
		color: #353535;
	}
</style>
