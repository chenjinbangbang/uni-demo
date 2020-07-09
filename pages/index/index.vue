<template>
	<view class="index">
		<!-- <view class="intro">本项目已包含uni ui组件，无需import和注册，可直接使用。在代码区键入字母u，即可通过代码助手列出所有可用组件。光标置于组件名称处按F1，即可查看组件文档。</view>
		<text class="intro">详见：</text> -->
		<!-- <uni-link :href="href" :text="href"></uni-link> -->

		<!-- <Text class="to-login" @tap="toLogin">您还未登录，请前往登录</Text> -->

		<button size="mini" type="primary" @tap="advertFn">查看广告获取收益</button>
	</view>
</template>

<script>
export default {
	data() {
		return {
			href: 'https://uniapp.dcloud.io/component/README?id=uniui',
			ad: null
		};
	},
	onReady() {
		
		// 广告初始化
		// console.log(uni.createRewardedVideoAd)
		if (uni.createRewardedVideoAd) {
			let ad = null;
			ad = uni.createRewardedVideoAd({
				adUnitId: '3o96jcmou957963398'
			});

			// 广告拉取成功
			ad.onLoad(() => {
				console.log('onLoad event');
			});

		// 	// 广告拉取失败
		// 	ad.onError(err => {
		// 		console.log('onError event', err);
		// 	});

		// 	// 监听用户关闭广告
		// 	ad.onClose(res => {
		// 		console.log('onClose event', res);
		// 		if (res && res.isEnded) {
		// 			console.log('广告正常播放结束');
		// 		} else {
		// 			console.log('广告中途播放退出');
		// 		}
		// 	});
		// 	this.ad = ad;
		}
	},
	methods: {
		toLogin() {
			uni.navigateTo({ url: '/pages/login/index' });
		},
		// 查看广告获取收益
		advertFn() {
			// 显示广告
			this.ad
				.show()
				.then(() => {
					console.log('激励视频 广告显示');
				})
				.catch(err => {
					console.log('显示广告失败', err);

					// 手动重新拉取广告
					this.ad
						.load()
						.then(() => {
							ad.show();
						})
						.catch(err => {
							console.log('');
						});
				});
		}
	}
};
</script>

<style lang="scss">
.index {
	padding: 20px;
	font-size: 14px;
	line-height: 24px;
	.to-login {
		color: #007aff;
	}
}
</style>
