<template>
	<view class="h100" v-if="isjihs">
		<scroll-view scroll-y="true" class="h100" :refresher-triggered="triggered" :refresher-threshold="100"
		 @refresherpulling="onPulling" @refresherrefresh="onRefresh" @refresherrestore="onRestore" @refresherabort="onAbort"
		 @scrolltolower="jjhseer">
			<view class="">
				<view class="pd">
					<view class="parentse ">
						<navigator class="cdderrty pr" v-for="sd in SongList" :url='"/pages/index/geshouxq?name=" + sd.SingerName + "&femian="+sd.ImagePaths+"&id="+sd.Id'>
							<image :lazy-load="true" :src="sd.ImagePaths" mode="aspectFill" v-if="sd.ImagePath"></image>
							<image src="../../../static/img/morentx.png" mode="aspectFill" v-else></image>
							<view class="kjhxer ">
								{{sd.SingerName}}
							</view>
						</navigator>
					</view>
				</view>
			</view>
			<uni-load-more iconType="snow" :iconSize="36" :status="loading" v-if="SongList.length>19&&jhjhsd" />
			<view class="fz26 z9 cen pt20" v-if="SongList.length<20 &&SongList.length>1 || !jhjhsd">
				------
			</view>
			<view v-if="sfgftyyd">
				<view class="fz26 z9 cen pt20" v-if="SongList.length<=0">
					{{kjhx.EmptyData}}
				</view>
			</view>
		</scroll-view>
	</view>
</template>
<script>
	import geshou from "@/static/js/dayys.js"
	export default {
		data() {
			return {
				sfgftyyd:false,
				jhjhsd:true,
				isjihs: false,
				jhjhsde:0,
				chuci: false,
				SongList: [],
				triggered: true,
				_freshing: false,
				pages: 1,
				loading: 'more',
				idxse: 0
			}
		},
		computed: {
			kjhx() {
				return this.$store.state.lanser
			}
		},
		components: {

		},
		methods: {
			async kkjsdddv(a, b, c, d) {
				this.sfgftyyd=false
				if (this.SongList.length < 20 && this.chuci) {
					return
				}
				let sdeer = await this.post(a, b, c, d)
				this.jhjhsde = JSON.parse(sdeer.MessageContent).SingerList.length
				JSON.parse(sdeer.MessageContent).SingerList.map(a => {
					if (!a.IsSelected) {
						a.IsSelected = false
						a.ImagePaths = uni.getStorageSync('gcook').ImageAddress + a.ImagePath
						a.cls = ""
					} else {
						a.cls = "act"
					}
					this.SongList.push(a)
				})
				this.isjihs = true
				this.loading = "more"
				this.sfgftyyd = true
			},
			hhsf(idx) {
				this.idxse = idx
			},
			initd() {
				let hhgsd = {}
				hhgsd.Value = null
				hhgsd.SingerLangId = this.$store.state.SingerLangId
				hhgsd.SingerTypeId = this.$store.state.SingerTypeId
				hhgsd.Value = this.$store.state.seartext
				hhgsd.PageNo = this.pages
				hhgsd.ListCount = 20
				this.kkjsdddv("vod/server/sendmessage", 'Search-Singer', hhgsd, 2)
			},
			iqhjwr() {
				this.SongList = []
				this.pages = 1
				this.jhjhsd = true
				this.initd()
			},
			onPulling(e) {},
			async onRefresh() {
				if (this._freshing) return;
				this._freshing = true;
				setTimeout(() => {
					this.triggered = false;
					this._freshing = false;
				}, 2000)
			},
			onAbort() {
				console.log("onAbort");
			},
			onRestore() {
				this.SongList = []
				this.triggered = 'restore'; // 需要重置
				this.pages = 1
				this.initd()
			},
			jjhseer(e) {
				console.log(this.jhjhsde)
				if (this.SongList.length < 20 ||this.jhjhsde<20) {
					this.jhjhsd = false
					return
				}
				this.pages++
				this.loading = "loading"
				this.initd()
			}
		},
		mounted() {
			this.$store.state.SingerTypeId = 1
			this.initd()
		}
	}
</script>
<style scoped>
	.kjhggdert {
		border-radius: 20upx;
		font-size: 26upx;
		padding: 6upx 20upx;
		background: #F2F2F2;
		color: #666;
		margin-right: 30upx;
		margin-bottom: 20upx;
	}

	.kjhggdert.act {
		color: #fff;
		background: #FFD33E;
	}

	.cdderrty {
		height: 280upx;
	}

	.cdderrty image {
		height: 100%;
		width: 100%;
		border-radius: 8upx;
	}

	.parentse {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-template-rows: 1fr;
		grid-column-gap: 40upx;
		grid-row-gap: 40upx;
	}

	.kjhxer {
		position: absolute;
		width: 100%;
		left: 0;
		bottom: 0;
		line-height: 50upx;
		color: #fff;
		font-size: 28upx;
		background: rgba(0, 0, 0, 0.5);
		text-align: center;
	}
</style>
