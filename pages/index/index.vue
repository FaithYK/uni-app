<template>
	<view id="help">
		<view class="oper-list">
			<view class="select-list">
				<view @click="allTask" class="text active">
					{{this_type.name+''}}
					<image :class="is_type?'active':''" class="icon" src="../../static/img/help/donw.png"></image>
				</view>
				<view @click="noviceZone" :class="param.order===5?'active':''" class="text">新手区</view>
				<view @click="masterZone" :class="param.order===2?'active':''" class="text">高手区</view>
			</view>
			<view class="seek-box">
				<image class="icon" src="../../static/img/help/seek.png"></image>
				<input @input="searchTask" class="seek-input" type="text" :value="param.search"></input>
			</view>
			<view :class="is_type?'active':''" class="type-list">
				<text @click="selectTaskType(item)" :class="item.id===this_type.id?'active':''" class="item"
					v-for="(item,index) in type_list" :key="item.id">{{item.name}}</text>
			</view>
		</view>
		<view class="help-center">
			<view class="item" v-for="(item,index) in data_list" :key="index">
				<task-item @toTask="toTask(item.id)" :info="item" :index="index"></task-item>
			</view>
			<view class="loading-more" v-if="data_list.length > 6">
				<text class="loading-more-text">{{is_data?'数据加载中···':'没有数据了···'}}</text>
			</view>
			<a-no-data v-if="data_list.length===0"></a-no-data>
			<!-- <uni-transition></uni-transition> -->
		</view>
	</view>
</template>

<script>
	import nodata from '../../components/noData/noData.vue'
	import taskItem from '../../components/task-item/task-item.vue'
	import aNoData from '../../components/a-noData/a-noData.vue'
	// import uniTransition from '../../components/uni-transition/uni-transition.vue'
	export default {
		components: {
			nodata,
			taskItem,
			aNoData
			// uniTransition
		},
		data() {
			return {
				this_type: {
					id: 0,
					name: "全部任务"
				},
				is_type: false,
				param: {
					page: 1,
					page_size: 20,
					type_id: 0,
					order: 0,
					search: ""
				},
				isRed: 1,
				type_list: [{
					id: 0,
					name: "全部",
				}, {
					id: 1,
					name: "简单注册"
				}, {
					id: 2,
					name: "合成试玩"
				}, {
					id: 3,
					name: "砍价助力"
				}, {
					id: 4,
					name: "实名金融"
				}, {
					id: 5,
					name: "关注涨粉"
				}],
				data_list: [],
				is_data: true
			}
		},
		onLoad() {
			//获取首页列表数据
			this.getDataList()
		},
		methods: {
			getDataList: function() {
				this.data_list = [{
						id: 0,
						is_top: true,
						head_img: '',
						title: '简单一分钟任务',
						type_name: '简单注册',
						proj_name: '点淘',
						ready_num: '29',
						total_num: '37',
						price: '30'
					},
					{
						id: 1,
						is_top: true,
						head_img: '',
						title: '简单版1分钟！',
						type_name: '简单注册',
						proj_name: '点淘',
						ready_num: '29',
						total_num: '37',
						price: '6'
					},
					{
						id: 2,
						is_top: true,
						head_img: '',
						title: '不下载扫码就过',
						type_name: '简单注册',
						proj_name: '有钱花',
						ready_num: '29',
						total_num: '37',
						price: '8'
					},
					{
						id: 3,
						is_top: true,
						head_img: '',
						title: '抖音砍价超简单',
						type_name: '简单注册',
						proj_name: '抖音',
						ready_num: '29',
						total_num: '37',
						price: '30'
					},
					{
						id: 4,
						is_top: true,
						head_img: '',
						title: '百度简单测试',
						type_name: '简单注册',
						proj_name: '有钱花',
						ready_num: '29',
						total_num: '37',
						price: '0.6'
					},
					{
						id: 5,
						is_top: true,
						head_img: '',
						title: '来登录下 秒过',
						type_name: '简单注册',
						proj_name: '苏宁易购',
						ready_num: '29',
						total_num: '37',
						price: '30'
					},
					{
						id: 6,
						is_top: true,
						head_img: '',
						title: '简单一分钟任务',
						type_name: '简单注册',
						proj_name: '点淘',
						ready_num: '29',
						total_num: '37',
						price: '25'
					}
				]
			},
			//显示全部任务
			allTask: function() {
				console.log('展示任务列表')
				this.is_type = !this.is_type
			},
			//选择任务分类
			selectTaskType: function(item) {
				console.log(item)
				this.this_type = item;
				this.is_type = false
			},
			//切换新手区
			noviceZone: function() {

			},
			//切换高手区
			masterZone: function() {

			},
			//搜索任务
			searchTask: function(event) {
				console.log(event.target.value)
				this.param.search = event.target.value
				console.log(this.param)
			},
			toTask: function(index) {
				console.log(index)
				uni.navigateTo({
					url: '../task/taskInfo?id=' + index
				})
			}

		}
	}
</script>

<style>
	#help {
		box-sizing: border-box;
		position: relative;
	}

	#help .oper-list {
		box-sizing: border-box;
		width: 100%;
		height: 100rpx;
		padding: 0 30rpx;
		border: 1rpx solid #f4f5f9;
		-webkit-box-align: center;
		align-items: center;
		position: fixed;
		background: #fff;
		left: 0;
		z-index: 3;
	}

	#help .oper-list,
	#help .oper-list .select-list {
		display: flex;
	}

	#help .oper-list .select-list {
		-webkit-box-pack: justify;
		justify-content: space-between;
		-webkit-box-flex: 1;
		flex: 1;
	}

	#help .oper-list .select-list .text {
		font-size: 32rpx;
		color: #000;
		line-height: 48rpx;
		font-weight: 700;
	}

	#help .oper-list .select-list .text.active {
		color: #307cf8;
	}

	#help .oper-list .select-list .text .icon {
		width: 48rpx;
		height: 48rpx;
		display: inline-block;
		float: right;
		transition: all .3s;
		margin-left: 10rpx;
	}

	#help .oper-list .select-list .text .icon.active {
		transform: rotate(180deg);
	}

	#help .oper-list .seek-box {
		width: 200rpx;
		height: 60rpx;
		background: #f4f5f9;
		margin-left: 54rpx;
		border-radius: 10rpx;
		padding: 0 20rpx;
		box-sizing: border-box;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
	}

	#help .oper-list .seek-box .icon {
		width: 48rpx;
		height: 48rpx;
	}

	#help .oper-list .seek-box .seek-input {
		width: 1;
		-webkit-box-flex: 1;
		flex: 1;
		height: 100%;
		font-size: 32rpx;
	}

	#help .oper-list .type-list {
		width: 320rpx;
		position: absolute;
		z-index: 9;
		top: 98rpx;
		left: 24rpx;
		background: #fff;
		box-shadow: 0rpx 8rpx 40rpx -7rpx rgba(112, 144, 176, .4);
		padding: 0 50rpx;
		box-sizing: border-box;
	}

	#help .oper-list .type-list::before {
		content: "";
		width: 0;
		height: 0;
		border-left: 20rpx solid transparent;
		border-right: 20rpx solid transparent;
		border-bottom: 0 solid #fff;
		position: absolute;
		left: 50%;
		transform: translateX(-50%);
		z-index: -1;
		top: -20rpx;
		box-shadow: 0rpx 8rpx 20rpx -7rpx rgba(112, 144, 176, .4);
	}

	#help .oper-list .type-list .item {
		display: block;
		text-align: center;
		background: #fff;
		line-height: 80rpx;
		color: #353535;
		font-size: 32rpx;
		height: 0;
		overflow: hidden;
		transition: all .5s;
		border: 0;
	}

	#help .oper-list .type-list .item.active {
		color: #307cf8;
	}

	#help .oper-list .type-list .item::after {
		content: "";
		width: 100%;
		height: 0rpx;
		background-color: #f4f5f9;
	}

	#help .oper-list .type-list.active {
		max-height: 100vh;
		overflow: initial;
	}

	#help .oper-list .type-list.active::before {
		border-bottom: 20rpx solid #fff;
	}

	#help .oper-list .type-list.active .item {
		height: 80rpx;
	}

	#help .oper-list .type-list.active .item::after {
		content: "";
		width: 100%;
		height: 1rpx;
	}

	#help .help-center {
		height: auto;
		min-height: 100vh;
		background: #f4f5f9;
		padding: 100rpx 30rpx 0;
	}

	#help .help-center .item {
		width: 336rpx;
		margin-right: 18rpx;
		margin-bottom: 18rpx;
		display: inline-block;
	}

	#help .help-center .item:nth-child(2n) {
		margin-right: 0;
	}
</style>
