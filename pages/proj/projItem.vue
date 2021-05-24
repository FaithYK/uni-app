<template>
	<view class="proj-item">
		<label :class="index<1?'active':''" class="index _span">{{index}}</label>
		<view class="info">
			<image class="logo" mode="aspectFit" :src="info.logo"></image>
			<view class="r">
				<view class="name">{{info.project_name}}</view>
				<view class="time">{{info.online_time}}</view>
			</view>
		</view>
		<view class="focus-num">{{info.focus_num}}</view>
		<view class="focus">
			<image @click="already" class="icon" src="../../static/img/proj/focus.png" v-if="info.is_focus"></image>
			<image @click="focusFn(info.project_id,index)" class="icon" src="../../static/img/proj/focus-no.png" v-else></image>
		</view>
	</view>

</template>

<script>
	export default {
		props: {
			info: Object,
			index: Number
		},
		data() {
			return {

			}
		},
		methods: {
			focusFn: function(n, e) {
				this.$emit("focus", n, e);
			},
			already: function() {
				n.showToast({
					title: "您以为该项目点过赞了",
					icon: "none"
				});
			}
		}
	}
</script>

<style lang="scss">
	.proj-item {
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		padding: 38rpx 0;
		border-top: 1px solid #f4f5f9;
	}

	.proj-item .index {
		width: 55rpx;
		font-size: 36rpx;
		text-align: center;
		color: #b2b2b2;
	}

	.proj-item .index.active {
		color: #307cf8;
	}

	.proj-item .info {
		-webkit-box-flex: 1;
		flex: 1;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-pack: center;
		justify-content: center;
		padding-left: 40rpx;
	}

	.proj-item .info .logo {
		width: 60rpx;
		height: 60rpx;
		display: block;
		border-radius: 50%;
		overflow: hidden;
	}

	.proj-item .info .r {
		-webkit-box-flex: 1;
		flex: 1;
		padding-left: 20rpx;
	}

	.proj-item .info .name {
		font-size: 30rpx;
		line-height: 1;
		color: #333;
		margin-bottom: 15rpx;
	}

	.proj-item .info .time {
		line-height: 1;
		font-size: 24rpx;
		color: #b2b2b2;
	}

	.proj-item .focus-num {
		width: 150rpx;
		text-align: center;
		font-size: 28rpx;
		color: #333;
	}

	.proj-item .focus {
		width: 120rpx;
	}

	.proj-item .focus .icon {
		width: 58rpx;
		height: 58rpx;
		float: right;
	}
</style>
