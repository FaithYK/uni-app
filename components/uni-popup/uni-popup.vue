<template>
	<view catchtouchmove="__e" :class="['uni-popup data-v-21dec862',popupstyle]" v-if="showPopup">
		<uni-transition bind:__l="__l" bind:click="__e" class="data-v-21dec862" :duration="duration"
			:modeClass="['fade']" v-show="showTrans" :styles="maskClass" v-if="maskShow">
		</uni-transition>
		<uni-transition bind:__l="__l" bind:click="__e" class="data-v-21dec862" :duration="duration" :modeClass="ani"
			v-show="showTrans" :styles="transClass" <view catchtap="__e" class="uni-popup__wrapper-box data-v-21dec862">
	</view>
	</uni-transition>
	</view>
</template>

<script>
	import uniTransition from '../uni-transition/uni-transition.vue'
	export default {
		name: "UniPopup",
		components: {
			uniTransition
		},
		components: {
			uniTransition: function() {
				o.e("components/uni-transition/uni-transition").then(function() {
					return resolve(o("36de"));
				}.bind(null, o)).catch(o.oe);
			}
		},
		props: {
			animation: {
				type: Boolean,
				default: true
			},
			type: {
				type: String,
				default: "center"
			},
			maskClick: {
				type: Boolean,
				default: true
			}
		},
		provide: function() {
			return {
				popup: this
			};
		},
		mixins: [i.default],
		watch: {
			type: {
				handler: function(t) {
					this[this.config[t]]();
				},
				immediate: !0
			},
			maskClick: function(t) {
				this.mkclick = t;
			}
		},
		data: function() {
			return {
				duration: 300,
				ani: [],
				showPopup: false,
				showTrans: false,
				maskClass: {
					position: "fixed",
					bottom: 0,
					top: 0,
					left: 0,
					right: 0,
					backgroundColor: "rgba(0, 0, 0, 0.4)"
				},
				transClass: {
					position: "fixed",
					left: 0,
					right: 0
				},
				maskShow: !0,
				mkclick: !0,
				popupstyle: "top"
			};
		},
		created: function() {
			this.mkclick = this.maskClick, this.animation ? this.duration = 300 : this.duration = 0;
		},
	}
</script>

<style>
	.uni-popup.data-v-21dec862 {
		position: fixed;
		z-index: 99;
	}

	.uni-popup__mask.data-v-21dec862 {
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		background-color: rgba(0, 0, 0, .4);
		opacity: 0;
	}

	.mask-ani.data-v-21dec862 {
		transition-property: opacity;
		transition-duration: .2s;
	}

	.uni-bottom-mask.data-v-21dec862,
	.uni-center-mask.data-v-21dec862,
	.uni-top-mask.data-v-21dec862 {
		opacity: 1;
	}

	.uni-popup__wrapper.data-v-21dec862 {
		display: block;
		position: absolute;
	}

	.top.data-v-21dec862 {
		top: 0;
	}

	.bottom.data-v-21dec862 {
		bottom: 0;
	}

	.uni-popup__wrapper-box.data-v-21dec862 {
		display: block;
		position: relative;
		padding-bottom: env(safe-area-inset-bottom);
	}

	.content-ani.data-v-21dec862 {
		transition-property: opacity, -webkit-transform;
		transition-property: transform, opacity;
		transition-property: transform, opacity, -webkit-transform;
		transition-duration: .2s;
	}

	.uni-bottom-content.data-v-21dec862,
	.uni-top-content.data-v-21dec862 {
		transform: translateY(0);
	}

	.uni-center-content.data-v-21dec862 {
		transform: scale(1);
		opacity: 1;
	}
</style>
