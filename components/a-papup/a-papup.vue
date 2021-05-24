<template>
	<view>
		<uni-popup @change="change" class="vue-ref">
			<view class="popup-content">
				<view class="common" v-if="show_content.type==='com'">
					<image class="com-img" src="../../static/img/popup/com.png"></image>
					<text class="text" v-if="show_content.msg">{{show_content.msg}}</text>
					<text class="text" v-else>小程序暂不支持该功能，请到App内操作</text>
					<button @click="openAPP" class="new-but" v-if="show_content.msg">咨询客服</button>
					<button appParameter="squirrelhelp" binderror="launchAppError" @click="openAPP" class="new-but"
						openType="launchApp" v-else>复制APP下载链接</button>
				</view>
				<view :class="['alert',show_content.class]" v-else>
					<image class="icon" :src="alert_icon[show_content.type]"></image>
					<view class="title" v-if="show_content.title">{{show_content.title}}</view>
					<text class="text" v-if="show_content.msg">{{show_content.msg}}</text>
					<view class="button-list">
						<button @click="realFn" class="but" type="default" v-for="(item,index) in show_content.button"
							:key="index">{{item}}</button>
					</view>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '../uni-popup/uni-popup.vue'
	export default {
		name: "a-papup",
		components: {
			'uni-popup': uniPopup
		},
		props: {
			placeholder: String
		},
		data() {
			return {
				alert_icon: {
					error: "../../static/img/popup/error.png",
					win: "../../static/img/popup/win.png"
				},
				type: "center",
				show_content: {
					class: "",
					title: "",
					msg: "",
					button: []
				}
			};
		}
	}
</script>

<style lang="scss">
	.popup-content {
		background: #fff;
		width: max-content;
		height: max-content;
		border-radius: 20rpx;
	}

	.popup-content .alert {
		min-width: 450rpx;
		min-height: 350rpx;
		box-sizing: border-box;
		position: relative;
		padding: 70rpx 40rpx;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-orient: vertical;
		-webkit-box-direction: normal;
		flex-direction: column;
		-webkit-box-pack: center;
		justify-content: center;
	}

	.popup-content .alert .icon {
		width: 125rpx;
		height: 125rpx;
		display: block;
		position: absolute;
		left: 50%;
		top: 0;
		transform: translate(-50%, -50%);
	}

	.popup-content .alert .title {
		font-size: 36rpx;
		color: #000;
		line-height: 70rpx;
		display: block;
		text-align: center;
		font-weight: 700;
	}

	.popup-content .alert .text {
		font-size: 32rpx;
		color: #000;
		line-height: 42rpx;
		display: block;
		margin: 70rpx 0;
		text-align: center;
	}

	.popup-content .alert .button-list {
		width: 100%;
		display: flex;
		-webkit-box-pack: justify;
		justify-content: space-between;
	}

	.popup-content .alert .button-list .but {
		width: 240rpx;
		height: 80rpx;
		line-height: 80rpx;
		background: #307cf8;
		color: #fff;
		font-size: 36rpx;
		border-radius: 10rpx;
		display: inline-block;
	}

	.popup-content .alert .button-list .but:first-child {
		border: 1px solid #307cf8;
		color: #307cf8;
		background: #fff;
	}

	.popup-content .real {
		width: 620rpx;
	}

	.popup-content .common,
	.popup-content .real {
		box-sizing: border-box;
	}

	.popup-content .common {
		max-width: 620rpx;
		width: 540rpx;
		position: relative;
		padding: 100rpx 40rpx;
	}

	.popup-content .common .com-img {
		width: 682rpx;
		height: 224rpx;
		display: block;
		position: absolute;
		left: 50%;
		top: -118rpx;
		transform: translate(-50%);
	}

	.popup-content .common .text {
		font-size: 32rpx;
		color: #000;
		line-height: 42rpx;
		display: block;
		margin: 70rpx 0;
		text-align: center;
	}

	.popup-content .common .new-but {
		width: 400rpx;
		height: 80rpx;
		line-height: 80rpx;
		background: #307cf8;
		color: #fff;
		font-size: 36rpx;
		border-radius: 10rpx;
	}
</style>
