<template>
	<view @click="change" :class="['uni-transition vue-ref',ani.in]" ref="ani"
		:style="'transform:'+transform+';'+stylesObject" v-if="isShow">
		<slot></slot>
	</view>
</template>

<script>
	export default {
		name: "uniTransition",
		props: {
			show: {
				type: Boolean,
				default: false
			},
			modeClass: {
				type: Array,
				default: () => {
					return [];
				}
			},
			duration: {
				type: Number,
				default: 300
			},
			styles: {
				type: Object,
				default: () => {
					return {};
				}
			}
		},
		data() {
			return {
				isShow: true,
				transform: "",
				ani: {
					in: "",
					active: ""
				}
			}
		},
		watch: {
			show: {
				handler: function(t) {
					// t ? this.open() : this.close();
				},
				immediate: !0
			}
		},
		computed: {
			stylesObject: function() {
				// var t = o(o({}, this.styles), {}, {
				// 		"transition-duration": this.duration / 1e3 + "s"
				// 	}),
				// 	n = "";
				// for (var e in t) n += this.toLine(e) + ":" + t[e] + ";";
				// return n;
			}
		},
		created: function() {},
	}
</script>

<style>
	.uni-transition {
		transition-timing-function: ease;
		transition-duration: .3s;
		transition-property: opacity, -webkit-transform;
		transition-property: transform, opacity;
		transition-property: transform, opacity, -webkit-transform;
	}

	.fade-in {
		opacity: 0;
	}

	.fade-active {
		opacity: 1;
	}

	.slide-top-in {
		transform: translateY(-100%);
	}

	.slide-top-active {
		transform: translateY(0);
	}

	.slide-right-in {
		transform: translateX(100%);
	}

	.slide-right-active {
		transform: translateX(0);
	}

	.slide-bottom-in {
		transform: translateY(100%);
	}

	.slide-bottom-active {
		transform: translateY(0);
	}

	.slide-left-in {
		transform: translateX(-100%);
	}

	.slide-left-active {
		transform: translateX(0);
		opacity: 1;
	}

	.zoom-in-in {
		transform: scale(.8);
	}

	.zoom-out-active {
		transform: scale(1);
	}

	.zoom-out-in {
		transform: scale(1.2);
	}
</style>
