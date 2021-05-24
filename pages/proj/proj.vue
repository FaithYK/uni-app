<template>
	<view :class="tab_index===0?'active':''" class="container proj-index">
		<!--可移动按钮-发布我的群-->
		<movable-area :class="tab_index===0?'active':''" class="movable-area">
			<movable-view class="movable" direction="all" :inertia="true" :outOfBounds="true" :x="1000" :y="500">
				<image @click="topubProj" class="icon" src="../../static/img/proj/pub.png"></image>
			</movable-view>
		</movable-area>
		<!--搜索框-->
		<view class="seek search">
			<a-seek @clickSeek="clickSeek" placeholder="输入项目查询档案"></a-seek>
		</view>
		<!--项目类型切换：项目交流|热门项目|新出项目-->
		<view class="index-tabber">
			<a-tab-ber @ontabtap="ontabtap" :tabBars="tab_bars" :tabIndex="tab_index"></a-tab-ber>
		</view>
		<!--热门项目界面top-->
		<view class="up-date" v-if="show_tab">以下数据仅供参考</view>
		<view class="label" v-if="show_tab">
			<label class="item _span">排名</label>
			<label class="item _span">项目名</label>
			<label class="item _span">热度值</label>
			<label class="item _span">点赞</label>
		</view>
		<!--内容-->
		<view class="content">
			<swiper @change="ontabchange" class="swiper-box" :current="tab_index" :duration="300">
				<swiper-item class="swiper-item" v-for="(tab,index1) in tab_bars" :key="index1">
					<scroll-view @scrolltolower="loadMore(index1)" class="scroll-v" :enableBackToTop="true"
						:scrollY="true">
						<view :class="tab_bars[index1].type===0?'invite':''" class="item" v-if="data_list.length"
							v-for="(item,index) in data_list" :key="index">
							<invite-item :index="index" :info="item" v-if="tab_bars[index1].type===0">
							</invite-item>
							<block v-else>
								<proj @focus="focus" @already="already" :index="index+1" :info="item"
									v-if="tab_bars[index1].type===1">
								</proj>
								<new-proj :info="item" :isTime="isTime" v-else>
								</new-proj>
							</block>
						</view>
						<!-- <view class="loading-more" v-if="tab[$orig].data.length">
							<text class="loading-more-text">{{tab[$orig].loadingText}}</text>
						</view> -->
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import Aseek from '../../components/a-seek/a-seek.vue'
	import bgTabber from '../../components/a-tabber/bg-tabber.vue'
	import inviteItem from './inviteItem.vue'
	import newProj from './newProj.vue'
	import proj from './projItem.vue'
	export default {
		components: {
			"a-seek": Aseek,
			"a-tab-ber": bgTabber,
			"invite-item": inviteItem,
			"new-proj": newProj,
			"proj": proj
		},
		data() {
			return {
				tab_index: 0,
				tab_bars: [{
					name: "项目交流",
					id: "xmjl",
					type: 0,
					share: "团队长都在这里推项目"
				}, {
					name: "热门项目",
					id: "rmxm",
					type: 1,
					share: "这些项目大家都在关注"
				}, {
					name: "新出项目",
					id: "xcxm",
					type: 2,
					share: "新出首码项目一览"
				}],
				data_list: [],
				share_title: "团队长都在这里推项目",
				isDoRefresh: false,
				share_path: "",
				isTime: {
					now: false,
					yes: false
				}
			}
		},
		computed: {
			show_tab: function() {
				return 1 === this.tab_index;
			},
		},
		onLoad() {
			var a = 0;
			var b = 1;
			if(a=b){
				console.log(a)
				console.log(b)
			}
			this.data_list = [{
					id: 0,
					sort: true,
					status: true,
					head_img: '',
					nickname: '周炳横',
					top_time: '2021-08-24 12:59',
					project_name: 'zhidian交易所',
					content: 'dog空投币(值钱了) 1、dog下一个百倍币 2、登陆APP',
					imgs: ['https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg'],
					qrcode_group: 'https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg'
				},
				{
					id: 1,
					sort: true,
					status: true,
					head_img: '',
					nickname: '九九',
					top_time: '2021-08-24 12:59',
					project_name: '穆奇卡[免单]',
					content: '穆奇卡(免单了) 1、穆奇卡下一个穆奇卡 2、登陆APP',
					imgs: ['https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg'],
					qrcode_group: 'https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg'
				}
			]
		},
		methods: {
			//项目切换
			ontabtap(e) {
				this.tab_index = e
				this.switchTab(e);
			},
			ontabchange: function(e) {
				var a = e.target.current || e.detail.current;
				this.switchTab(a);
			},
			switchTab: function(t) {
				if (this.tab_index !== t) {
					if (this.share_title = this.tab_bars[t].share, this.tab_index = t,
					 this.scrollInto = this.tab_bars[
							t].id,
						0 === this.data_list.length) return false;
				}
				switch (t) {
					case 0:
						this.data_list = [{
								id: 0,
								sort: true,
								//是否在审核中
								status: true,
								head_img: '',
								nickname: '周炳横',
								top_time: '2021-08-24 12:59',
								project_name: 'zhidian交易所',
								content: 'dog空投币(值钱了) 1、dog下一个百倍币 2、登陆APP',
								imgs: ['https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg', ''],
								qrcode_group: 'https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg'
							},
							{
								id: 1,
								sort: true,
								status: true,
								head_img: '',
								nickname: '九九',
								top_time: '2021-08-24 12:59',
								project_name: '穆奇卡[免单]',
								content: '穆奇卡(免单了) 1、穆奇卡下一个穆奇卡 2、登陆APP',
								imgs: ['https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg', ''],
								qrcode_group: 'https://i.loli.net/2021/05/19/BbHRycA69dL5jf7.jpg'
							}
						]
						break;
					case 1:
						this.data_list = [{
								project_id: 0,
								logo: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3159209942,1733010480&fm=26&gp=0.jpg',
								project_name: '拍呱呱',
								online_time: '上线5个月',
								focus_num: 1550115,
								is_focus: true
							},
							{
								project_id: 1,
								logo: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3717120934,3932520698&fm=26&gp=0.jpg',
								project_name: '快步',
								online_time: '上线13个月',
								focus_num: 145417,
								is_focus: true
							}
						]
						break;
					case 2:
						this.data_list = [{
								id: 0,
								publish_time: '2021-08-24 12:59',
								//是否在审核中
								status: true,
								border: true,
								head_img: '',
								published: true,
								project_name: 'EC功链'
							},
							{
								id: 1,
								publish_time: '2021-08-24 12:59',
								status: true,
								border: true,
								head_img: '',
								published: true,
								project_name: 'ECccc功链'
							}
						]
						break;
				}
			},
			listFn: function(a) {
				console.log(a)
				// var n = this;
				// if (1 === this.data_list[a].param.page && (this.data_list[a].data = [], this.data_list[a].isLoading = !
				// 		1),
				// 	this.data_list[a].isLoading) return false;
			},
			clickSeek(e) {
				console.log(this.tab_index)
				console.log(e)
				this.data_list[this.tab_index].param.app_name = e,
					this.data_list[this.tab_index].param.page = 1,
					this.listFn(this.tab_index);
			}
		}
	}
</script>

<style lang="scss">
	.container {
		display: flex;
		-webkit-box-orient: vertical;
		-webkit-box-direction: normal;
		flex-direction: column;
		width: 100vw;
		height: 100vh;
	}

	.content {
		-webkit-box-flex: 1;
		flex: 1;
		width: 100%;
		height: 1px;
		overflow: hidden;
	}

	.pl {
		color: #b2b2b2;
	}

	button::after {
		border: none;
	}

	._img {
		width: 100%;
	}

	.loading-more .loading-more-text {
		font-size: 28rpx;
		color: #999;
	}

	.proj-index {
		background: #fff;
	}

	.proj-index.active {
		background: #f4f5f9;
	}

	.proj-index .index-tabber {
		height: 100rpx;
		box-sizing: border-box;
		padding: 18rpx 30rpx;
		background: #fff;
	}

	.proj-index .movable-area {
		position: fixed;
		width: 100vw;
		height: 100vh;
		top: 0;
		left: 0;
		pointer-events: none;
		z-index: -1;
	}

	.proj-index .movable-area .movable {
		width: 162rpx;
		height: 119rpx;
		display: block;
		z-index: -1;
		pointer-events: auto;
	}

	.proj-index .movable-area .movable .icon {
		width: 100%;
		height: 100%;
		display: block;
	}

	.proj-index .movable-area.active {
		z-index: 9;
	}

	.proj-index .seek {
		background: #307cf8;
		padding: 13rpx 30rpx 16rpx;
	}

	.proj-index .up-date {
		background: #f7f7f7;
		padding: 0 30rpx;
		font-size: 24rpx;
		line-height: 44rpx;
		color: #b2b2b2;
	}

	.proj-index .label {
		padding: 14rpx 30rpx 0;
		line-height: 58rpx;
		font-size: 30rpx;
		display: flex;
	}

	.proj-index .label .item {
		text-align: center;
	}

	.proj-index .label .item:nth-child(1) {
		width: 70rpx;
		text-align: left;
	}

	.proj-index .label .item:nth-child(2) {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
		text-align: left;
		padding-left: 90rpx;
	}

	.proj-index .label .item:nth-child(3) {
		width: 150rpx;
	}

	.proj-index .label .item:nth-child(4) {
		width: 120rpx;
		text-align: right;
	}

	.proj-index .content .item {
		padding: 0 30rpx;
	}

	.proj-index .content .item.invite {
		padding: 0;
	}

	.swiper-box {
		height: 100%;
		width: 100%;
	}

	.swiper-item {
		flex: 1;
		-webkit-box-orient: horizontal;
		flex-direction: row;
	}

	.scroll-v,
	.swiper-item {
		-webkit-box-flex: 1;
		-webkit-box-direction: normal;
	}

	.scroll-v {
		flex: 1;
		-webkit-box-orient: vertical;
		flex-direction: column;
		width: 100%;
		height: 100%;
	}

	.refresh {
		width: 750rpx;
		height: 64px;
	}

	.refresh,
	.refresh-view {
		-webkit-box-pack: center;
		justify-content: center;
	}

	.refresh-view {
		-webkit-box-orient: horizontal;
		-webkit-box-direction: normal;
		flex-direction: row;
		flex-wrap: nowrap;
		-webkit-box-align: center;
		align-items: center;
	}

	.refresh-icon {
		width: 30px;
		height: 30px;
		transition-duration: .5s;
		transition-property: transform;
		transition-property: transform, -webkit-transform;
		transform: rotate(0deg);
		transform-origin: 15px 15px;
	}

	.refresh-icon-active {
		transform: rotate(180deg);
	}

	.loading-icon {
		width: 20px;
		height: 20px;
		margin-right: 5px;
		color: #999;
	}

	.loading-text {
		margin-left: 2px;
		font-size: 18px;
		color: #999;
	}

	.loading-more {
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-pack: center;
		justify-content: center;
		padding-top: 10px;
		padding-bottom: 10px;
		text-align: center;
	}

	.loading-more-text {
		font-size: 30rpx;
		color: #999;
	}
</style>
