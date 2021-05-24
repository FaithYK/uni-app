<template>
	<view class="news">
		<view class="seek">
			<a-seek @clickSeek="clickSeek" placeholder="搜索相关资讯"></a-seek>
		</view>
		<view class="news-list">
			<view class="item" v-for="(item,i) in data_list" :key="i">
				<news-item :info="item" @toNewsDetail="toNewsDetail"></news-item>
			</view>
			<view class="loading-more" v-if="data_list.length>6">
				<text class="loading-more-text">{{is_data?'数据加载中···':'没有数据了···'}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	import aSeek from '../../components/a-seek/a-seek.vue'
	import newsItem from './newsItem.vue'

	export default {
		components: {
			"a-seek": aSeek,
			"news-item": newsItem
		},
		data() {
			return {
				data_list: [{
						id: 0,
						title: '[爆料]“BSD”刷量交易所又一个“头寸管理”....',
						img: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3717120934,3932520698&fm=26&gp=0.jpg',
						intro: '评论盘：最近大量粉丝留言爆料“BSD”刷量交易所这个资金盘，差点怎么怎么怎么了',
						add_time: '2021-05-20 01:36:45',
						view_num: 459
					},
					{
						id: 1,
						title: '[骗局]拍呱呱买矿机？韭菜们最无助的叹息！',
						img: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3159209942,1733010480&fm=26&gp=0.jpg',
						intro: '评论盘：最近大量粉丝留言爆料“BSD”刷量交易所这个资金盘，差点怎么怎么怎么了',
						add_time: '2021-05-19 01:36:45',
						view_num: 559
					}, {
						id: 2,
						title: '[哈哈哈]哈哈哈买矿机？韭菜们最无助的叹息！',
						img: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3717120934,3932520698&fm=26&gp=0.jpg',
						intro: '||干货||黑幕||骗局||揭秘||真实 客户限制哈哈哈',
						add_time: '2021-05-17 01:36:45',
						view_num: 659
					}
				],
				is_data: false
			}
		},
		mounted() {

		},
		onLoad() {
			console.log(this.data_list.length)
		},
		methods: {
			toNewsDetail(e){
				uni.navigateTo({
					url:  'newsDetail?id='+ e
				})
			}
		}
	}
</script>

<style lang="scss">
	.news {
		min-height: 100vh;
	}

	.news .seek {
		background: #307cf8;
		padding: 13rpx 30rpx 16rpx;
		box-sizing: border-box;
		width: 100%;
		position: fixed;
		left: 0;
		z-index: 9;
	}

	.news .news-list {
		padding-top: 94rpx;
	}

	.news .news-list .item {
		padding: 0 30rpx;
	}
</style>
