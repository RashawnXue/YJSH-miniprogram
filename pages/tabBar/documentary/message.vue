<template>
	<view>
		<web-view :src="ads"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				address:[
				"https://mp.weixin.qq.com/s/udGy4TkSa_iY6dxaI90sJA",
				"https://mp.weixin.qq.com/s/eR984p6riNhuZjzIxuCPSQ",
				"https://mp.weixin.qq.com/s/_xbYksrPwVfLnSwz8zu10Q",
				"https://mp.weixin.qq.com/s/TzgFelJ9Lu2BDR9xf5yl8A",
				"https://mp.weixin.qq.com/s/l2LcRhWVK_IuVHnOq4WZWA"
				],
				ads:"",
			}
		},
		onLoad(options) {
			this.ads=this.address[options.num];
		},
		onShow() {
			console.log(this.ads);
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
