<template>
	<div>
		<uni-modal v-if="kjhsd">
			<view class="uni-mask"></view>
			<div class="uni-modal">
				<div class="uni-modal__bd">当前会话已过期, 请重新扫二维码!</div>
			</div>
		</uni-modal>
	</div>
</template>
<script>
	export default {
		data() {
			return {
				kjhsd:false
			}
		},
		components: {},
		methods: {
			async getdatas() {
				let hhgghse = await this.get('https://oybab.net/wechat/GM')
				if (!hhgghse.Lang) {
					this.kjhsd = true
					// uni.showModal({
					// 	content: this.$store.state.lanser.ExpiredDescription,
					// 	showCancel: false,
					// 	confirmText: this.$store.state.lanser.OK,
					// 	success: function(res) {}
					// });
					uni.hideLoading()
					return
				}
				uni.setStorage({
					key: 'gcook',
					data: hhgghse,
					success: () => {
						let sdr = uni.getStorageSync('lanindex')
						// 设置缓存过期时间
						let sdee = new Date().getTime()
						uni.setStorageSync('times', sdee)
						this.$store.commit('setlanser', sdr || 0)
						uni.switchTab({
							url: '/pages/index/index'
						})
						uni.hideLoading()
					}
				})
			}
		},
		onLoad: () => {

		},
		mounted() {
			uni.showLoading({
				title: 'loader...'
			})

			var ddfer = uni.getStorageSync('gcook')
			this.getdatas()
		}
	}
</script>
<style lang='scss' scoped>

</style>
