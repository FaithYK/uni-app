<template>
	<view class="bg-tab-bar">
		<text class="bg"
			:style="'width:'+100/tabBars.length+'%'+';'+'left:'+100/tabBars.length*tab_index+'%'+';'"></text>
		<view @click="ontabtap(index)" class="tab-item" :class="tab_index===index?'active':''"
			v-for="(tab,index) in tabBars" :key="tab.id">{{tab.name}}</view>
	</view>
</template>

<script>
	export default {
		name: "bg-tabber",
		props: {
			tabBars: Array,
			tabIndex: Number,
			border: String
		},
		data() {
			return {
				cacheTab: [],
				scrollInto: "",
				tab_index: 0
			};
		},
		mounted: function() {
			this.tab_index = this.tabIndex;
		},
		methods: {
			ontabtap: function(index) {
				this.tab_index = index,
					this.$emit("ontabtap", index);
			}
		},
		watch: {
			tabIndex: function(t) {
				this.tab_index = t,
					this.scrollInto = this.tabBars[t].id,
					console.log(this.scrollInto);
			}
		}
	}
</script>

<style lang="scss">
	.bg-tab-bar {
		text-align: center;
		overflow: hidden;
		-webkit-box-orient: horizontal;
		-webkit-box-direction: normal;
		flex-direction: row;
		white-space: nowrap;
		background: #f8f8f8;
		display: flex;
		position: relative;
	}

	.bg-tab-bar,
	.bg-tab-bar .bg {
		width: 100%;
		height: 100%;
		border-radius: 100rpx;
	}

	.bg-tab-bar .bg {
		position: absolute;
		background: #307cf8;
		left: 0;
		top: 0;
	}

	.bg-tab-bar .bg,
	.bg-tab-bar .tab-item {
		transition: all .3s;
	}

	.bg-tab-bar .tab-item {
		-webkit-box-flex: 1;
		flex: 1;
		width: 1rpx;
		height: 100%;
		overflow: hidden;
		border-radius: 100rpx;
		display: flex;
		-webkit-box-align: center;
		align-items: center;
		-webkit-box-pack: center;
		justify-content: center;
		font-size: 32rpx;
		color: #292929;
		position: relative;
	}

	.bg-tab-bar .tab-item.active {
		color: #fff;
	}
</style>
