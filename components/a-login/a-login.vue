<template>
	<view>
		<uni-popup @change="change" class="vue-ref">
			<view class="popup-content">
				<view class="popup-login" v-if="!is_code_bind">
					<image class="logo" src="../../static/img/login/logo.png"></image>
					<image class="text" src="../../static/img/login/text.png"></image>
					<button bindgetuserinfo="getuserinfo" class="login-but" openType="getUserInfo" type="default"
						withCredentials="true" v-:if="!is_login">
						<image class="wx" src="../../static/img/login/wx.png"></image>微信登录
					</button>
					<block wx:else>
						<view class="bind-phone" v-if="!is_bind_phone">
							<button bindgetphonenumber="__e" class="bind-but" openType="getPhoneNumber">一键绑定手机号</button>
							<button @click="codeBindFn" class="code-but">验证码绑定手机号</button>
						</view>
					</block>
				</view>
				<view class="code-bind" v-else>
					<view class="bind-input">
						<input @input="phoneNum" class="input" placeholder="请输入手机号" type="number"
							:value="code_info.phone_num"></input>
					</view>
					<view class="bind-input">
						<input @input="setModel" class="input" placeholder="请输入验证码" type="text"
							:value="code_info.code"></input>
						<code-but class="code-but" :phone="code_info.phone_num"></code-but>
					</view>
					<view class="button-list">
						<button @click="codeBindPhoneFn" class="button">确定</button>
						<button @click="codeBindFn" class="button return">返回</button>
					</view>
				</view>
				<view class="protocol">登录即表示同意松鼠帮帮<text @click="toServe" class="protocol1">《用户协议》</text>
					<text @click="toPrivacy" class="protocol1">《隐私政策》</text>
				</view>
			</view>
		</uni-popup>

	</view>
</template>

<script>
	import uniPopup from '../uni-popup/uni-popup.vue'
	export default {
		name: "a-login",
		components: {
			'uni-popup': uniPopup
		},
		data() {
			return {
				is_login: false,
				is_bind_phone: false,
				is_code_bind: false,
				code_info: {
					phone_num: "",
					code: ""
				}
			};
		}
	}
</script>

<style lang="scss">
	.popup-content {
		background: url(data:image/png;base64,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) no-repeat 50%;
		background-size: cover;
		width: 620rpx;
		height: 670rpx;
		border-radius: 20rpx;
		box-sizing: border-box;
		position: relative;
	}

	.popup-content .popup-login {
		width: 100%;
		padding: 120rpx 0 30rpx;
	}

	.popup-content .popup-login .logo {
		width: 110rpx;
		height: 110rpx;
		display: block;
		margin: 0 auto;
	}

	.popup-content .popup-login .text {
		width: 143rpx;
		height: 34rpx;
		display: block;
		margin: 30rpx auto 0;
	}

	.popup-content .popup-login .login-but {
		width: 470rpx;
		height: 80rpx;
		border-radius: 10rpx;
		background: #307cf8;
		color: #fff;
		font-size: 36rpx;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-pack: center;
		justify-content: center;
		margin: 98rpx auto 0;
	}

	.popup-content .popup-login .login-but .wx {
		width: 50rpx;
		height: 40rpx;
		margin-right: 20rpx;
	}

	.popup-content .popup-login .bind-phone .bind-but,
	.popup-content .popup-login .bind-phone .code-but {
		width: 470rpx;
		height: 80rpx;
		border-radius: 10rpx;
		background: #307cf8;
		color: #fff;
		font-size: 36rpx;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-pack: center;
		justify-content: center;
		margin: 30rpx auto 0;
	}

	.popup-content .popup-login .bind-phone .code-but {
		background: #fff;
		border: 1px solid #307cf8;
		color: #307cf8;
	}

	.popup-content .code-bind {
		width: 470rpx;
		margin: auto;
		padding: 90rpx 0 0;
	}

	.popup-content .code-bind .title {
		font-size: 36rpx;
		text-align: center;
		font-weight: 700;
		margin-bottom: 40rpx;
	}

	.popup-content .code-bind .bind-input {
		width: 100%;
		height: 100rpx;
		background: #f4f5f9;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		margin-bottom: 30rpx;
		padding: 0 20rpx;
		box-sizing: border-box;
		border-radius: 10rpx;
		overflow: hidden;
	}

	.popup-content .code-bind .bind-input .input {
		height: 100%;
		font-size: 32rpx;
	}

	.popup-content .code-bind .bind-input .code-but {
		width: 103rpx;
		height: 60rpx;
		background: #307cf8;
		font-size: 28rpx;
		padding: 0;
		color: #fff;
		line-height: 60rpx;
		text-align: center;
		border-radius: 6rpx;
	}

	.popup-content .code-bind .button-list {
		padding-top: 30rpx;
	}

	.popup-content .code-bind .button-list .button {
		margin-bottom: 20rpx;
		height: 80rpx;
		border-radius: 10rpx;
		font-size: 36rpx;
		color: #fff;
		background: #307cf8;
	}

	.popup-content .code-bind .button-list .return {
		background: #fff;
		border: 1px solid #307cf8;
		color: #307cf8;
	}

	.popup-content .protocol {
		font-size: 26rpx;
		color: #858585;
		position: absolute;
		bottom: 0;
		left: 0;
		padding: 30rpx;
		text-align: center;
		width: 100%;
		box-sizing: border-box;
	}

	.popup-content .protocol .protocol1 {
		color: #000;
	}
</style>
