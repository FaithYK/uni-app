<template>
	<view class="no-data">
		<image mode="" class="errer" src="../../static/img/error.png"></image>
		<view class="text _p">{{text}}</view>
	</view>
</template>

<script>
	export default {
		nam: 'aNoData',
		props: {
			text: {
				type: String,
				default: "暂无数据"
			}
		},
		
	}
</script>

<style>
	.no-data {
		width: 100%;
		height: auto;
		padding: 200rpx 0 0;
	}

	.no-data .errer {
		width: 200rpx;
		height: 190rpx;
		display: block;
		margin: 0 auto;
	}

	.no-data .text {
		text-align: center;
		font-size: 32rpx;
		color: #b2b2b2;
	}
</style>
