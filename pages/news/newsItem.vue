<template>
	<view class="news-item" @click="toNewsDetail(info.id)" >
		<view class="title">{{info.title}}</view>
		<view class="info">
			<image class="banner" mode="aspectFill" :src="info.img" v-if="info.img"></image>
			<view class="intro-time">
				<view class="intro">{{info.intro}}</view>
				<view class="time">{{'时间：'+info.add_time+'     浏览：'+info.view_num+''}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "newsItem",
		props: {
			info: Object
		},
		data() {
			return {

			};
		},
		methods:{
			toNewsDetail(id){
				this.$emit("toNewsDetail",id)
			}
		}
	}
</script>

<style lang="scss">
	.news-item {
		padding: 38rpx 0;
		border-bottom: 1px solid #f4f5f9;
	}

	.news-item .title {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		font-size: 34rpx;
		color: #000;
		line-height: 1;
	}

	.news-item .info {
		padding-top: 20rpx;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
	}

	.news-item .info .banner {
		width: 220rpx;
		height: 150rpx;
		margin-right: 20rpx;
	}

	.news-item .info .intro-time {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
	}

	.news-item .info .intro {
		font-size: 30rpx;
		color: #888;
		overflow: hidden;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
	}

	.news-item .info .time {
		font-size: 22rpx;
		color: #b2b2b2;
		margin-top: 20rpx;
	}
</style>
