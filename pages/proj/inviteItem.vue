<template>
	<view :class="!info.status?'verify':''" class="invite-item">
		<view :class="info.sort?'active':''" class="user">
			<image class="top" mode="aspectFill" src="../../static/img/help/top.png" v-if="info.sort"></image>
			<image class="face" mode="aspectFill" :src="info.head_img||logo"></image>
			<text class="name">{{info.nickname||'小松鼠'}}</text>
			<text class="time" v-if="info.sort">{{'置顶至'+info.top_time}}</text>
		</view>
		<view class="invite-content">
			<view class="text">
				<view @click="toLink(info.pub_id,info.project_name)" class="active" v-if="showName">
					<image class="p" src="../../static/img/proj/p.png"></image>{{'#'+info.project_name+'#'}}
				</view>
				<text>{{info.content}}</text>
			</view>
			<view  class="img-list">
				<image @click="previewImage(0)" class="img" mode="aspectFill" :src="info.qrcode_group"
					v-if="info.qrcode_group"></image>
				<image @click="previewImage(1)" class="img" mode="aspectFill" :src="info.qrcode_user"
					v-if="info.qrcode_user"></image>
				<image @click="previewImage(i + 2)" class="img" mode="aspectFill" :src="img"
					v-for="(img,i) in info.imgs" :key="i"></image>
			</view>
			<view class="oper" v-if="info.is_edit">
				<image @click="operFn" class="oper-but" src="../../static/img/oper.png"></image>
				<view :class="show_oper?'active':''" class="oper-list">
					<view @click="toLink($root.g0)" class="oper-item" 编辑</view>
					</view>
				</view>
			</view>
		</view>

</template>

<script>
	export default {
		props: {
			info: Object,
			index: Number,
			showName: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				logo: "../../static/img/logo_.png",
				show_oper: false,
				class_list: ["one", "two", "three", "four"]
			}
		},
		methods: {
			donwLoadApp: function() {
				this.$emit("donwLoadApp");
			},
			previewImage: function(n) {
				console.log(n);
				for (var e = [this.info.qrcode_group, 
				this.info.qrcode_user],
				 t = this.info.imgs, i = 0; i < t.length; i++) 
				 e.push(t[i]);
				console.log(e), o.previewImage({
					urls: e,
					current: e[n]
				});
			},
			operFn: function() {
				this.show_oper = !this.show_oper;
			},
			deleFn: function(n, e) {
				console.log(n);
				var t = this;
				t.del_info = {
					id: n,
					index: e
				}, o.showModal({
					title: "",
					content: "删除后不可恢复,是否确认删除？",
					success: function(o) {
						o.confirm ? (console.log("点击了确认"), t.$emit("del", n, e)) : console.log("点击了取消");
					}
				});
			}
		}
	}
</script>

<style lang="scss">
	.invite-item {
		width: 100%;
		position: relative;
		margin-top: 16rpx;
		background: #fff;
		border-radius: 10rpx;
		overflow: hidden;
	}

	.invite-item.verify::after {
		content: "";
		width: 150rpx;
		height: 150rpx;
		display: block;
		position: absolute;
		top: 40rpx;
		right: 0rpx;
		background: url(data:image/png;base64,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) no-repeat 50%;
		background-size: cover;
		z-index: 1;
	}

	.invite-item .user {
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		padding: 0 30rpx;
		height: 80rpx;
		position: relative;
	}

	.invite-item .user.active {
		padding: 0 30rpx 0 64rpx;
		background: linear-gradient(131deg, #ff6a46, #ffb259);
	}

	.invite-item .user.active .name,
	.invite-item .user.active .time {
		color: #fff;
	}

	.invite-item .user .face {
		width: 72rpx;
		height: 72rpx;
		border-radius: 100rpx;
		display: block;
		border: 1rpx solid #fff;
		position: relative;
	}

	.invite-item .user .name {
		font-size: 28rpx;
		color: #000;
		padding-left: 10rpx;
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
	}

	.invite-item .user .time {
		font-size: 22rpx;
		color: #000;
	}

	.invite-item .user .top {
		position: absolute;
		width: 100rpx;
		height: 80rpx;
		top: 0;
		left: 0;
	}

	.invite-item .invite-content {
		padding: 0 24rpx 20rpx;
	}

	.invite-item .invite-content .text {
		line-height: 42rpx;
		font-size: 32rpx;
		color: #353535;
		padding: 20rpx 0;
		word-break: break-all;
		display: block;
	}

	.invite-item .invite-content .text .active {
		font-size: 32rpx;
		color: #307cf8;
		font-weight: 700;
		position: relative;
		background: #f8f8f8;
		display: inline-block;
		padding: 0 10rpx 0 46rpx;
		line-height: 42rpx;
		border-radius: 6rpx;
	}

	.invite-item .invite-content .text .active .p {
		width: 31rpx;
		height: 36rpx;
		position: absolute;
		top: 50%;
		left: 10rpx;
		transform: translateY(-50%);
	}

	.invite-item .img-list {
		width: 100%;
		height: auto;
		display: flex;
		flex-wrap: wrap;
		max-height: 405rpx;
	}

	.invite-item .img-list.active {
		max-height: 190rpx;
	}

	.invite-item .img-list .img {
		width: 190rpx;
		height: 190rpx;
		margin-right: 25rpx;
		margin-bottom: 25rpx;
	}

	.invite-item .img-list .img:nth-child(3n) {
		margin-right: 0;
	}

	.invite-item .oper {
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		height: 70rpx;
		padding-top: 10rpx;
	}

	.invite-item .oper .oper-but {
		width: 50rpx;
		height: 30rpx;
		margin-right: 15rpx;
	}

	.invite-item .oper .oper-list {
		width: 0rpx;
		height: 60rpx;
		overflow: hidden;
		background: rgba(0, 0, 0, .5);
		border-radius: 6rpx;
		color: #fff;
		font-size: 28rpx;
		line-height: 60rpx;
		transition: all .3s;
		display: flex;
	}

	.invite-item .oper .oper-list.active {
		width: 140rpx;
	}

	.invite-item .oper .oper-list .oper-item {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
		display: inline-block;
		text-align: center;
		position: relative;
		padding: 0;
	}

	.invite-item .oper .oper-list .oper-item::before {
		content: "";
		width: 1rpx;
		height: 40rpx;
		position: absolute;
		display: block;
		right: 0;
		top: 50%;
		background: #fff;
		transform: translateY(-50%);
	}

	.invite-item .oper .oper-list .oper-item:last-child::before {
		width: 0;
	}
</style>
