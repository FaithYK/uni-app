<template>
	<view class="search-box">
		<view class="search">
			<image class="seek-icon" src="../../static/img/seek.png"></image>
			<image @click="clear" class="clear" src="../../static/img/qk.png" v-if="val"></image>
			<input @input="input" class="seek-input" :placeholder="placeholder" placeholderClass="pl" type="text"
				:value="val"></input>
		</view>
		<button @click="seekFn" class="button" type="default">搜索</button>
	</view>
</template>

<script>
	export default {
		name: "a-seek",
		props: {
			placeholder: String
		},
		data() {
			return {
				val: ""
			};
		},
		methods: {
			seekFn: function() {
				this.$emit("clickSeek", this.val);
			},
			clearFn: function() {
				this.val = "";
			}
		}
	}
</script>

<style lang="scss">
	.search-box,
	.search-box .search {
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		position: relative;
	}

	.search-box .search {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
	}

	.search-box .search .seek-icon {
		left: 20rpx;
	}

	.search-box .search .clear,
	.search-box .search .seek-icon {
		width: 44rpx;
		height: 44rpx;
		background: #fff;
		position: absolute;
	}

	.search-box .search .clear {
		right: 20rpx;
	}

	.search-box .search .seek-input {
		width: 100%;
		background: #fff;
		height: 64rpx;
		border-radius: 10rpx;
		font-size: 28rpx;
		padding: 0 70rpx;
	}

	.search-box .button {
		background: hsla(0, 0%, 100%, 0);
		height: 64rpx;
		line-height: 64rpx;
		color: #fff;
		font-size: 36rpx;
		padding: 0 0 0 20rpx;
	}

	.search-box .button::after {
		border: 0;
	}
</style>
