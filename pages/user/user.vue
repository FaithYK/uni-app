<template>
	<view class="container" id="user">
		<view class="user-top">
			<view class="header">松鼠帮帮</view>
			<view @click="toLink" class="user-info" v-if="!login_info.is_login">
				<image class="face" src="../../static/img/user/face.png"></image>
				<!--#ifdef MP-WEIXIN-->
				<view class="user">
					<text class="no-name">获取微信头像</text>
				</view>
				<!--#endif-->
				<!--#ifdef APP-PLUS || H5-->
				<view class="user">
					<text class="no-name">登录</text>
				</view>
				<!--#endif-->
			</view>
			<!--#ifdef MP-WEIXIN-->
			<view class="user-info" v-else>
				<image class="face" :src="info.head_img"></image>
				<view class="user">
					<view class="name">
						<text class="text">{{info.nickname}}</text>
					</view>
					<text class="bind-phone" v-if="info.phone_num">{{'绑定手机号：'+$root.g0+'****'+$root.g1}}</text>
					<view class="me-code">{{'我的邀请码：'+info.uid+''}}<button @click="copyUrl(info.uid)" class="copy"
							type="default">复制</button>
					</view>
				</view>
			</view>

			<view class="wallet">{{'我的钱包：￥'+(info.remain||'--')+''}}
				<button @click="donwLoadApp" class="extract" type="default">提现</button>
			</view>
			<!--#endif-->
			<!--#ifdef H5 || APP-PLUS-->
			<view class="detail">
				<view class="info-detail">
					<view style="display: flex;flex-direction: row;justify-content: space-between;">
						<view class="detail-num">
							<view>徒弟人数</view>
							<view><text>0</text>人</view>
						</view>
						<view class="detail-btn">查看明细</view>
					</view>
					<view class="line"></view>
					<view>累计收徒收益</view>
					<view><text>0.00</text>元</view>

				</view>
				<view class="info-detail">
					<view style="display: flex;flex-direction: row;justify-content: space-between;">
						<view class="detail-num">
							<view>钱包余额</view>
							<view><text>0.00</text>元</view>
						</view>
						<view class="detail-btn">查看明细</view>
					</view>
					<view class="line"></view>
					<view style="padding-top: 10rpx;">累计做单收入</view>
					<view><text>0.00</text>元</view>

				</view>
			</view>
			<!--#endif-->
		</view>
		<!--#ifdef MP-WEIXIN-->
		<view class="user-two">
			<view @click="totaskList" class="item">我发的单<image class="icon" src="../../static/img/user/1.png"></image>
			</view>
			<view @click="toacceptList" class="item">我接的单<image class="icon" src="../../static/img/user/2.png"></image>
			</view>
		</view>
		<view class="user-title">其他</view>
		<view class="user-item-list">
			<view @click="toivcode" class="user-item" v-if="info.show_code">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">填邀请码</text>
			</view>
			<view @click="toreal" class="user-item">
				<image class="icon" src="../../static/img/user/u1.png"></image>
				<text class="text">收款实名</text>
			</view>
			<view @click="toadvise" class="user-item">
				<image class="icon" src="../../static/img/user/u3.png"></image>
				<text class="text">客服留言</text>
			</view>
			<view @click="tocopyUrl('https://share.foretellmaster.com/share-ssbb/download')" class="user-item">
				<image class="icon" src="../../static/img/user/u5.png"></image>
				<text class="text">邀请下载</text>
			</view>
		</view>
		<!--#endif-->
		<!--#ifdef APP-PLUS || H5-->
		<view class="user-h5-two">
			<view @click="totaskList" class="item">我发的单</image>
			</view>
			<view @click="toacceptList" class="item">我接的单</image>
			</view>
			<view @click="totaskList" class="item">我发的项目群</image>
			</view>
			<view @click="toacceptList" class="item">我发的文章</image>
			</view>
		</view>
		<view class="user-title">其他</view>
		<view class="user-item-list" style="padding-bottom: 50px;">
			<view @click="toivcode" class="user-item">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">新手奖励</text>
			</view>
			<view @click="toivcode" class="user-item">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">推广赚钱</text>
			</view>
			<view @click="toivcode" class="user-item">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">游戏赚</text>
			</view>
			<view @click="toivcode" class="user-item">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">发单</text>
			</view>
			<view @click="toivcode" class="user-item">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">消息列表</text>
			</view>
			<view @click="toivcode" class="user-item">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">官方Q群</text>
			</view>
			<view @click="toadvise" class="user-item">
				<image class="icon" src="../../static/img/user/u3.png"></image>
				<text class="text">客服</text>
			</view>
			<view @click="toreal" class="user-item">
				<image class="icon" src="../../static/img/user/u1.png"></image>
				<text class="text">收款实名</text>
			</view>
			<view @click="toivcode" class="user-item">
				<image class="icon" src="../../static/img/user/u0.png"></image>
				<text class="text">版本更新</text>
			</view>
			<view @click="tocopyUrl('https://share.foretellmaster.com/share-ssbb/download')" class="user-item">
				<image class="icon" src="../../static/img/user/u5.png"></image>
				<text class="text">设置</text>
			</view>
		</view>
		<!--#endif-->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				login_info: {
					is_login: false
				},
				info: {}
			}
		},
		methods: {
			donwLoadApp() {

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

	#user {
		height: 100vh;
		background: #fff;
	}

	#user .user-top {
		background: url(data:image/png;base64,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) no-repeat bottom;
		background-size: cover;
		padding-top: 50rpx;
	}

	#user .user-top .header {
		font-size: 36rpx;
		color: #fff;
		text-align: center;
		line-height: 100rpx;
	}

	#user .user-top .user-info {
		width: 100%;
		height: 240rpx;
		display: flex;
		padding: 0 30rpx;
		box-sizing: border-box;
		margin-bottom: 16rpx;
	}

	#user .user-top .user-info .face {
		width: 110rpx;
		height: 110rpx;
		display: block;
		border-radius: 50%;
		margin-right: 30rpx;
	}

	#user .user-top .user-info .user {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
	}

	#user .user-top .user-info .user .no-name {
		color: #fff;
		font-size: 34rpx;
		line-height: 110rpx;
	}

	#user .user-top .user-info .user .name {
		color: #fff;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		padding-bottom: 5rpx;
	}

	#user .user-top .user-info .user .name .text {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
		font-size: 34rpx;
		color: #fff;
		padding-right: 5rpx;
	}

	#user .user-top .user-info .user .name .free {
		height: 40rpx;
		padding: 0 20rpx;
		background: -webkit-gradient(linear, right top, left top, from(#fd2922), to(#f55719));
		background: -webkit-linear-gradient(right, #fd2922, #f55719);
		background: linear-gradient(270deg, #fd2922, #f55719);
		border-radius: 20rpx;
		line-height: 40rpx;
		font-size: 26rpx;
		color: #fff;
	}

	#user .user-top .user-info .user .bind-phone {
		font-size: 28rpx;
		color: #fff;
		line-height: 50rpx;
		margin-top: 10rpx;
		display: block;
	}

	#user .user-top .user-info .user .me-code {
		font-size: 28rpx;
		color: #fff;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		margin-top: 10rpx;
	}

	#user .user-top .user-info .user .me-code .copy {
		width: 150rpx;
		height: 50rpx;
		padding: 0;
		line-height: 50rpx;
		background: inherit;
		color: #fff;
		font-size: 30rpx;
		border: 1rpx solid #fff;
		border-radius: 25rpx;
	}

	#user .user-top .wallet {
		width: 690rpx;
		background: -webkit-gradient(linear, left top, right top, from(#1b1b1b), to(#373535));
		background: -webkit-linear-gradient(left, #1b1b1b, #373535);
		background: linear-gradient(90deg, #1b1b1b, #373535);
		border-radius: 24rpx 24rpx 0 0;
		margin: 0 auto;
		line-height: 60rpx;
		color: #bf9774;
		font-size: 32rpx;
		padding: 18rpx 30rpx;
		box-sizing: border-box;
	}

	#user .user-top .detail {
		display: flex;
		flex-direction: row;
		box-sizing: border-box;
		width: 100%;
		height: 200rpx;
		padding: 18rpx 4rpx;
		position: absolute;
		margin-top: -60px;
	}

	#user .user-top .detail .info-detail {
		width: 320rpx;
		height: 90px;
		background: lightblue;
		margin: 0 8px;
		padding: 5px 0px 5px 10px;
		border-radius: 24rpx;
	}

	#user .user-top .detail .info-detail .detail-btn {
		width: 65px;
		height: 25px;
		background: $uni-color-primary;
		color: #FFFFFF;
		line-height: 25px;
		text-align: center;
		border-start-start-radius: 30rpx;
		border-end-start-radius: 30rpx;
		margin-top: 16rpx;
		font-size: 14px;
		right: 0;
	}

	#user .user-top .detail .info-detail view {
		font-size: 28rpx;
	}

	#user .user-top .detail .info-detail view text {
		color: $uni-color-primary;
	}

	#user .user-top .detail .info-detail .line {
		height: 1rpx;
		width: 300rpx;
		background: #000000;
		margin: 5px 0px;
	}

	#user .user-top .wallet .extract {
		width: 130rpx;
		height: 60rpx;
		background: -webkit-gradient(linear, right top, left top, from(#fcd1b3), to(#e5a77e));
		background: -webkit-linear-gradient(right, #fcd1b3, #e5a77e);
		background: linear-gradient(270deg, #fcd1b3, #e5a77e);
		border-radius: 30rpx;
		float: right;
		line-height: 60rpx;
		font-size: 32rpx;
		color: #292828;
	}

	#user .banner {
		padding: 20rpx 30rpx;
	}

	#user .banner .img {
		width: 100%;
		height: 146rpx;
		animation: masked-animation 1.5s infinite;
	}

	@-webkit-keyframes masked-animation {
		0% {
			transform: scale(.95);
		}

		50% {
			transform: scale(1.05);
		}

		100% {
			transform: scale(.95);
		}
	}

	#user .user-two {
		padding: 30rpx;
		flex-wrap: wrap;
	}

	#user .user-two,
	#user .user-two .item {
		display: flex;
		-webkit-box-pack: justify;
		justify-content: space-between;
	}

	#user .user-two .item {
		width: 330rpx;
		height: 140rpx;
		-webkit-box-align: center;
		align-items: center;
		padding: 0 30rpx;
		background: #fff;
		box-shadow: 0rpx 8rpx 40rpx -7rpx rgba(112, 144, 176, .44);
		border-radius: 24rpx;
		box-sizing: border-box;
		font-size: 32rpx;
		font-weight: 700;
		color: #292828;
	}

	#user .user-two .item .icon {
		width: 84rpx;
		height: 84rpx;
	}

	#user .user-h5-two {
		padding: 30rpx;
		flex-wrap: wrap;
		margin-top: 50px;
	}

	#user .user-h5-two,
	#user .user-h5-two .item {
		display: flex;
		-webkit-box-pack: justify;
		justify-content: space-between;
	}

	#user .user-h5-two .item {
		width: 330rpx;
		height: 140rpx;
		-webkit-box-align: center;
		align-items: center;
		padding: 0 30rpx;
		background: #fff;
		box-shadow: 0rpx 8rpx 40rpx -7rpx rgba(112, 144, 176, .44);
		border-radius: 24rpx;
		box-sizing: border-box;
		font-size: 32rpx;
		font-weight: 700;
		color: #292828;
		margin: 8px 0;
	}

	#user .user-title {
		font-size: 32rpx;
		color: #000;
		padding: 20rpx 30rpx;
		font-weight: 700;
	}

	#user .user-item-list {
		display: flex;
		flex-wrap: wrap;
	}

	#user .user-item-list .user-item {
		width: 25%;
		padding: 10rpx 0 20rpx;
		text-align: center;
		box-sizing: border-box;
	}

	#user .user-item-list .user-item .icon {
		width: 84rpx;
		height: 84rpx;
		margin: 0 auto 20rpx;
		display: block;
	}

	#user .user-item-list .user-item .text {
		font-size: 28rpx;
		color: #888;
		line-height: 37rpx;
	}

	#user .donw-load {
		width: 660rpx;
		height: 80rpx;
		border: 1px solid #307cf8;
		color: #307cf8;
		font-size: 30rpx;
		line-height: 80rpx;
		margin-top: 200rpx;
		border-radius: 10rpx;
	}

	#user .user-title-h5 {
		// position: relative;
		font-size: 32rpx;
		color: #000;
		padding: 20rpx 30rpx;
		font-weight: 700;
	}
</style>
