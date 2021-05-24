<template>
	<view class="proj-item">
		<view :class="isTime.now?'active':''" class="time">{{info.publish_time+'上线'}}</view>
		<view :class="[!info.status?'verify':'',border?'border':'']" class="item-cen">
			<view class="user">
				<view class="user-info">
					<view class="face-box">
						<image class="face" :src="info.head_img||logo"></image>
						<!-- <image ></image> -->
					</view>{{''+(info.nickname||'小松鼠')+'   爆料'}}
				</view>
				<image class="lately" src="../../static/img/proj/lately.png" v-if="!info.published&&info.status ">
				</image>
			</view>
			<view class="info">
				<view class="name">{{info.project_name}}</view>
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		props: {
			info: Object,
			isTime: Object,
			border: Boolean
		},
		data() {
			return {
				logo: "../../static/img/logo_.png",
			}
		},
		methods: {
			toLink: function(e) {
				this.info.status && n.navigateTo({
					url: e
				});
			},
			declareFn: function(n, e, o) {
				this.$emit("declare", n, e, o, this.index);
			}
		}
	}
</script>

<style lang="scss">
	.proj-item {
		width: 100%;
		padding-left: 50rpx;
		padding-bottom: 30rpx;
		box-sizing: border-box;
	}

	.proj-item .item-cen {
		background: #fff;
		box-shadow: 0rpx 8rpx 40rpx -7rpx rgba(112, 144, 176, .2);
		border-radius: 10px;
		padding: 34rpx 24rpx 38rpx;
		position: relative;
	}

	.proj-item .item-cen .user {
		-webkit-box-pack: justify;
		justify-content: space-between;
		padding: 0rpx 0 26rpx;
	}

	.proj-item .item-cen .user,
	.proj-item .item-cen .user .user-info {
		display: flex;
		-webkit-box-align: center;
		align-items: center;
	}

	.proj-item .item-cen .user .user-info {
		font-size: 32rpx;
		color: #888;
	}

	.proj-item .item-cen .user .user-info .face-box {
		display: inline-block;
		border-radius: 50%;
		width: 33rpx;
		height: 33rpx;
		overflow: hidden;
		position: relative;
		box-sizing: border-box;
		margin-right: 18rpx;
	}

	.proj-item .item-cen .user .user-info .face-box .face {
		width: 100%;
		height: 100%;
		display: block;
		border-radius: 50%;
		margin-right: 18rpx;
	}

	.proj-item .item-cen .user .lately {
		width: 138rpx;
		height: 36rpx;
		display: block;
	}

	.proj-item .item-cen .info {
		display: flex;
		-webkit-box-pack: justify;
		justify-content: space-between;
		-webkit-box-align: center;
		align-items: center;
	}

	.proj-item .item-cen .info .name {
		font-size: 36rpx;
		color: #fd2922;
		font-weight: 700;
	}

	.proj-item .item-cen .info .look {
		font-size: 32rpx;
		color: #353535;
	}

	.proj-item .item-cen::before {
		content: "";
		width: 1px;
		height: calc(100% + 80rpx);
		position: absolute;
		top: -22rpx;
		left: -40rpx;
		background: #b2b2b2;
	}

	.proj-item .item-cen.border::before {
		width: 0;
	}

	.proj-item .item-cen.verify::after {
		content: "";
		width: 80rpx;
		height: 83rpx;
		display: block;
		position: absolute;
		top: 0;
		right: 0rpx;
		background: url(data:image/png;base64,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) no-repeat 0 100%;
		background-size: cover;
		z-index: 1;
	}

	.proj-item .time {
		font-size: 28rpx;
		color: #353535;
		position: relative;
		padding: 10rpx 0;
	}

	.proj-item .time::before {
		content: "";
		width: 16rpx;
		height: 16rpx;
		left: -47rpx;
		top: 50%;
		transform: translateY(-50%);
		display: block;
		border-radius: 50%;
		background: #b2b2b2;
		position: absolute;
		z-index: 2;
	}

	.proj-item .time.active::before {
		width: 22rpx;
		height: 22rpx;
		left: -50rpx;
		background: #307cf8;
		z-index: 2;
	}
</style>
