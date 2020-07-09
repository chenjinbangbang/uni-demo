<template>
	<view>
		<button size="mini" type="primary" @tap="login">一键登录</button>
		<button size="mini" type="default" @tap="getUserInfo">获取用户信息</button>
	</view>
</template>

<script>
export default {
	data() {
		return {};
	},
	onReady(){
		// 检查登录状态是否过期
		// uni.checkSession({
		// 	success(res) {
		// 		console.log(res)
		// 	},
		// 	fail(err) {
		// 		console.log(err)
		// 	}
		// })
	},
	methods: {
		// 一键登录
		login() {
			// 获取服务提供商
			uni.getProvider({
				service: 'oauth',
				success(res) {
					console.log(res);
					
					if (res.provider.includes('toutiao')) {
						// 登录
						uni.login({
							provider: 'toutiao',
							success(res) {
								console.log(res);
								
								// 检查登录状态是否过期
								uni.checkSession({
									success(res) {
										console.log(res)
									}
								})
							},
							fail(err) {
								console.error(err);
							}
						});
					}
				},
				fail(err) {
					console.error(err);
				}
			});
		},
		// 获取用户信息
		getUserInfo(){
			uni.getUserInfo({
				provider: 'toutiao',
				withCredentials: true,
				success(res) {
					console.log(res)
				}
			})
		}
	}
};
</script>

<style lang="scss"></style>
