<template>
	<view v-if="kkjjsd">
		<view class="jhggxseert dx_jz w100 row cen">
			<view class="col">
				<view class="xwerrtxe fz30 z6 pr cen   f_b cz " :class="kjhse==0?'act':''" @tap="kjhse=0">
					{{kjhx.SelectedSongs}}
				</view>
			</view>
			<view class="col">
				<view class="xwerrtxe fz30 z6 pr cen   f_b cz" :class="kjhse==1?'act':''" @tap="kjhse=1">
					{{kjhx.SingedSongs}}
				</view>
			</view>
		</view>
		<view class="xrrtxeertx" :style="{height:xrrtxeertx+'px'}">
			<swiper class="h100" @change="jhxerert" :current="kjhse">
				<swiper-item >
					<component is="xzyypage" v-if="0==kjhse" urls="TheList-Selected" isyhgg="1" hggbbsd="3"></component>
				</swiper-item>
				<swiper-item >
					<component is="xzyypage" v-if="1==kjhse" urls="TheList-Singed" isyhgg=""></component>
				</swiper-item>
			</swiper>
		</view>
		<!-- <publiclist v-if="kjhse==1"></publiclist> -->
	</view>
</template>
<script>
	import publiclist from "@/components/publiclist.vue"
	import xzyypage from "@/pages/index/components/xzyypage.vue"
	export default {
		data() {
			return {
				kkjjsd:false,
				urlsd: ['TheList-Selected', 'TheList-Singed'],
				xrrtxeertx: '',
				kjhse: 0
			}
		},
		computed: {
			kjhx() {
				return this.$store.state.lanser
			}
		},
		components: {
			publiclist,
			xzyypage
		},
		methods: {
			jhxerert(e) {
				this.kjhse = e.detail.current
			}
		},
		onShow() {
			uni.setNavigationBarTitle({
			    title: this.kjhx.Selected
			})
			this.kkjjsd = true
		},
		onHide(){
			this.kkjjsd = false
		},	
		onLoad(e) {
			this.xrrtxeertx = uni.getSystemInfoSync().windowHeight - 50
		},
		mounted() {

		}
	}
</script>
<style>
</style>
<style scoped>
	.jhggxseert {
		top: 0;
	}

	.xwerrtxe {
		display: inline-block;
	}
</style>
