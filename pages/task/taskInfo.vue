<template>
	<view class="container" id="task-info" v-if="is_loading">
		<view class="content">
			<view class="task-info">
				<view class="task-one">
					<image class="top-img" src="../../static/img/help/top.png"></image>
					<image class="face" :src="info.head_img"></image>
					<view class="info">
						<view class="title">{{info.title+''}}</view>
						<view class="tag-list">
							<text class="tag">{{info.type_name}}</text>
							<text class="tag">{{info.proj_name}}</text>
						</view>
					</view>
					<view class="price">
						<text class="num">{{info.price}}</text>元
					</view>
				</view>
				<view class="task-two">
					<view class="item">
						<view class="cen">
							<text
								class="num">{{info.finish_time>24?info.finish_time/24:info.finish_time}}</text>{{''+(info.finish_time>24?'天':'小时')+''}}
						</view>
						<text class="text">交单限时</text>
					</view>
					<view class="item">
						<view class="cen">
							<text
								class="num">{{info.check_time>24?info.check_time/24:info.check_time}}</text>{{''+(info.check_time>24?'天':'小时')+''}}
						</view>
						<text class="text">审核周期</text>
					</view>
					<view class="item">
						<view class="cen">
							<text class="num">{{info.ready_num+'/'+info.total_num}}</text>人
						</view>
						<text class="text">已报名数</text>
					</view>
					<view class="item">
						<view class="cen">
							<text class="num">{{info.remain}}</text>元
						</view>
						<text class="text">已付保证金</text>
					</view>
				</view>
				<view class="task-three">
					<view class="clue">
						<image class="icon" src="../../static/img/help/1.png"></image>任务说明
					</view>
					<view class="intro">{{info.intro}}</view>
				</view>
				<view class="task-four">
					<view class="clue">
						<image class="icon" src="../../static/img/help/2.png"></image>任务步骤
					</view>
					<view class="step" v-for="(item,index) in info.finish_step" :key="index">
						<view class="text">
							<text class="cen">{{item.content+(item.web?item.web:'')}}</text>
							<button @click="copyUrl" class="copy-but" type="default">复制</button>
						</view>
						<view class="img-list" v-if="item.url">
							<view class="img-box">
								<text class="icon">说明图</text>
								<image @click="lookImg(info.finish_step,index,item.url)"
									:class="[info.btn.act===3&&index===0?'active':'']" class="img" mode="aspectFill"
									:src="item.url"></image>
								<view class="shade" v-if="[info.btn.act===3&&index===0]">请先接单</view>
							</view>
						</view>
					</view>
				</view>
				<view class="task-five">
					<view class="clue">
						<image class="icon" src="../../static/img/help/3.png"></image>上传验证
					</view>
					<view class="step" v-for="(item,index) in info.check_step" :key="index">
						<view class="text">{{item.content}}</view>
						<textarea :autoHeight="true" @cinput="__e" class="textarea"
							:disabled="info.btn.act!==4||info.btn.disable===2" maxlength="80"
							:placeholder="item.content" placeholderClass="pl" :value="info.upload_step[index].content"
							v-if="!item.url&&(info.btn.act>3||info.btn.act===0)"></textarea>
						<view class="img-list" v-if="item.url">
							<view class="img-box">
								<text class="icon">示例图</text>
								<image @click="lookImg(info.check_step,index,item.url)" class="img" mode="aspectFill"
									:src="item.url"></image>
							</view>
							<view @click="upImgFn" class="img-box" v-if="info.btn.act>3||info.btn.act===0">
								<view class="up-img" v-if="choose_img_url[index]===null">
									<image class="up" mode="aspectFill" src="../../static/img/help/up.png"></image>
									<text class="up-text">请上传验证截图</text>
								</view>
								<image class="img" mode="aspectFill" :src="choose_img_url[index]"
									v-if="choose_img_url[index]"></image>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="but-list" v-if="info.btn.disable!==2">
			<button @click="subFn(info.btn.act)" :class="info.btn.disable?'disabled':''" class="sub-but"
				:disabled="info.btn.disable?true:false" type="default">{{info.btn.value}}</button>
		</view>
		<a-login class="vue-ref"></a-login>
		<a-papup  @subBut="subBut" class="vue-ref"></a-papup>
	</view>
</template>

<script>
	import aLogin from '../../components/a-login/a-login.vue'
	import aPapup from '../../components/a-papup/a-papup.vue'
	export default {
		components:{
			"a-login": aLogin,
			"a-papup": aPapup
		},
		data() {
			return {
				is_loading: true,
				info: {},
				choose_img_url: [],
				choose_image: {
					count: 9,
					sourceType: ["camera", "album"],
					sizeType: ["compressed", "original"]
				},
				id: "",
				content: "",
				share_title: "“雇主昵称”+请你帮忙“任务类型”，做完给您“任务赏金”感谢金。",
				share_path: ""
			}
		},
		onLoad(options) {
			console.log("taskInfo: ", options)
			this.getInfoDetail()
		},
		methods: {
			getInfoDetail() {
				this.info = {
					head_img: '',
					title: '🔥新人必做🔥',
					type_name: '实名注册',
					proj_name: '陀螺世界',
					price: 3.3,
					finish_time: '3.00',
					check_time: '24.00',
					ready_num: 122,
					total_num: 403,
					remain: 1329.9,
					intro: '只限没有注册过“陀螺世界”的新手接单，如果已经注册过“陀螺世界”请勿接单，避免浪费时间，谢谢合作。',
					finish_step: [{
							content: '扫码下载，邀请码：tnjtxh',
							web: '',
							url: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3159209942,1733010480&fm=26&gp=0.jpg'
						},
						{
							content: '扫码下载，邀请码：tnjtxh',
							web: '',
							url: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3717120934,3932520698&fm=26&gp=0.jpg'
						}
					],
					check_step: [{
							content: '提现0.3元',
							url: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3159209942,1733010480&fm=26&gp=0.jpg'
						},
						{
							content: '看完15次视频截图',
							url: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3717120934,3932520698&fm=26&gp=0.jpg'
						}
					],
					btn: {
						act: 7,
						disable: 0,
						value: '我要接单赚钱'
					}
				}
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

	#task-info {
		background: #f4f5f9;
	}

	#task-info .task-info {
		width: 100%;
		height: 100%;
		overflow: auto;
	}

	#task-info .task-one {
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		margin-bottom: 16rpx;
		overflow: hidden;
		padding: 40rpx;
		background: #fff;
		position: relative;
	}

	#task-info .task-one .top-img {
		width: 120rpx;
		height: 91rpx;
		position: absolute;
		left: 0;
		top: 0;
	}

	#task-info .task-one .face {
		width: 100rpx;
		height: 100rpx;
		display: block;
		border-radius: 50%;
		background: url(data:image/png;base64,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) no-repeat 50%;
		background-size: cover;
	}

	#task-info .task-one .info {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
		min-height: 100rpx;
		display: flex;
		-webkit-box-orient: vertical;
		-webkit-box-direction: normal;
		flex-direction: column;
		-webkit-box-pack: justify;
		justify-content: space-between;
		padding-left: 24rpx;
	}

	#task-info .task-one .info .title {
		font-size: 32rpx;
		color: #000;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		line-height: 40rpx;
		font-weight: 700;
	}

	#task-info .task-one .info .title .top {
		margin-left: 10rpx;
		width: 62rpx;
		line-height: 40rpx;
		margin-right: 16rpx;
		font-size: 32rpx;
		text-align: center;
		position: relative;
		display: inline-block;
	}

	#task-info .task-one .info .title .top .top-img {
		position: absolute;
		width: 100%;
		height: 79rpx;
		bottom: -5rpx;
		left: 0;
	}

	#task-info .task-one .info .title .top .top-text {
		position: relative;
		line-height: 40rpx;
		z-index: 1;
		font-size: 22rpx;
		display: block;
		font-weight: 700;
		text-align: center;
		background: -webkit-linear-gradient(left, #147b96, #e6d205 25%, #e08309 50%, #ff2d08 75%, #4204ec);
		color: transparent;
		-webkit-background-clip: text;
		background-size: 200% 100%;
		animation: masked-animation 1s linear infinite;
	}

	#task-info .task-one .info .tag-list .tag {
		background: #ffefee;
		color: #f61d16;
		font-size: 24rpx;
		padding: 0 12rpx;
		line-height: 40rpx;
		display: inline-block;
		margin-right: 16rpx;
		margin-top: 10rpx;
	}

	#task-info .task-one .info .tag-list .tag:last-child {
		margin: 0;
	}

	#task-info .task-one .price {
		font-size: 24rpx;
		color: #fd2922;
	}

	#task-info .task-one .price .num {
		font-size: 60rpx;
		font-weight: 700;
	}

	#task-info .task-two {
		display: flex;
		-webkit-box-pack: justify;
		justify-content: space-between;
		padding: 0 30rpx;
		-webkit-box-align: center;
		align-items: center;
		height: 157rpx;
		background: #fff;
		margin-bottom: 16rpx;
	}

	#task-info .task-two .item {
		text-align: center;
	}

	#task-info .task-two .item .cen {
		font-size: 26rpx;
		color: #353535;
		line-height: 48rpx;
		margin-bottom: 15rpx;
		padding-right: 10rpx;
	}

	#task-info .task-two .item .cen .num {
		font-size: 46rpx;
		color: #000;
		font-weight: 700;
	}

	#task-info .task-two .item .text {
		color: #888;
		font-size: 26rpx;
		line-height: 33rpx;
	}

	#task-info .task-three {
		background: #fff;
		padding: 30rpx;
		margin-bottom: 16rpx;
	}

	#task-info .task-three .intro {
		font-size: 32rpx;
		color: #353535;
		padding-left: 48rpx;
		line-height: 42rpx;
	}

	#task-info .task-five,
	#task-info .task-four {
		background: #fff;
		padding: 30rpx;
		margin-bottom: 16rpx;
	}

	#task-info .task-five .step .text,
	#task-info .task-four .step .text {
		font-size: 32rpx;
		color: #353535;
		line-height: 40rpx;
		position: relative;
		padding-left: 48rpx;
		margin: 40rpx 0 20rpx;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		word-break: break-all;
	}

	#task-info .task-five .step .text .cen,
	#task-info .task-four .step .text .cen {
		padding-right: 5rpx;
		width: 1rpx;
		-webkit-box-flex: 1;
		flex: 1;
		word-break: break-all;
	}

	#task-info .task-five .step .text::before,
	#task-info .task-four .step .text::before {
		content: attr(data-name);
		width: 40rpx;
		height: 40rpx;
		display: inline-block;
		font-size: 32rpx;
		color: #fff;
		background: #307cf8;
		line-height: 40rpx;
		text-align: center;
		border-radius: 50%;
		position: absolute;
		left: 0;
		top: 1rpx;
	}

	#task-info .task-five .step .text .copy-but,
	#task-info .task-four .step .text .copy-but {
		height: 40rpx;
		font-size: 26rpx;
		color: #fff;
		background: #307cf8;
		border-radius: 6rpx;
		line-height: 40rpx;
		display: inline-block;
		padding: 0 20rpx;
	}

	#task-info .task-five .step .textarea,
	#task-info .task-four .step .textarea {
		width: 100%;
		border: 1px solid #ebebeb;
		min-height: 100rpx;
		padding: 20rpx 30rpx;
		box-sizing: border-box;
		border-radius: 10rpx;
		background: #f4f5f9;
		font-size: 32rpx;
	}

	#task-info .task-five .step .img-list,
	#task-info .task-four .step .img-list {
		padding: 0 48rpx;
		display: flex;
		-webkit-box-pack: justify;
		justify-content: space-between;
	}

	#task-info .task-five .step .img-list .img-box,
	#task-info .task-four .step .img-list .img-box {
		position: relative;
		width: 276rpx;
		height: 384rpx;
		overflow: hidden;
	}

	#task-info .task-five .step .img-list .img-box .up-img,
	#task-info .task-four .step .img-list .img-box .up-img {
		width: 100%;
		height: 100%;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-orient: vertical;
		-webkit-box-direction: normal;
		flex-direction: column;
		-webkit-box-pack: center;
		justify-content: center;
	}

	#task-info .task-five .step .img-list .img-box .up-img .up,
	#task-info .task-four .step .img-list .img-box .up-img .up {
		width: 88rpx;
		height: 88rpx;
		display: block;
	}

	#task-info .task-five .step .img-list .img-box .up-img .up-text,
	#task-info .task-four .step .img-list .img-box .up-img .up-text {
		font-size: 32rpx;
		color: #888;
		line-height: 62rpx;
	}

	#task-info .task-five .step .img-list .img-box .icon,
	#task-info .task-four .step .img-list .img-box .icon {
		position: absolute;
		right: 0;
		top: 0;
		background: #d6e2f7;
		border-radius: 6rpx;
		color: #307cf8;
		font-size: 28rpx;
		line-height: 42rpx;
		padding: 0 20rpx;
		z-index: 9;
	}

	#task-info .task-five .step .img-list .img-box .img,
	#task-info .task-four .step .img-list .img-box .img {
		width: 100%;
		height: 100%;
		border-radius: 6rpx;
	}

	#task-info .task-five .step .img-list .img-box .img.active,
	#task-info .task-four .step .img-list .img-box .img.active {
		filter: blur(10rpx);
	}

	#task-info .task-five .step .img-list .img-box .shade,
	#task-info .task-four .step .img-list .img-box .shade {
		position: absolute;
		width: 100%;
		height: 100%;
		background: hsla(0, 0%, 100%, .6);
		top: 0;
		left: 0;
		z-index: 8;
		color: #307cf8;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-pack: center;
		justify-content: center;
		font-size: 32rpx;
	}

	#task-info .sub-but {
		width: 690rpx;
		height: 80rpx;
		background: #307cf8;
		color: #fff;
		font-size: 36rpx;
		line-height: 80rpx;
		border-radius: 10rpx;
		margin: 30rpx auto;
	}

	#task-info .sub-but.disabled {
		background: #ccc;
	}

	#task-info .clue {
		font-size: 32rpx;
		font-weight: 700;
		color: #307cf8;
		line-height: 48rpx;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
	}

	#task-info .clue .icon {
		width: 48rpx;
		height: 48rpx;
		display: inline-block;
	}

	@-webkit-keyframes masked-animation {
		0% {
			background-position: 0 0;
		}

		100% {
			background-position: -100% 0;
		}
	}
</style>
