<template>
	<view class="h100" v-if="isjihs">
		<scroll-view scroll-y="true" class="h100"  :refresher-triggered="triggered"
		 :refresher-threshold="100" @refresherpulling="onPulling" @refresherrefresh="onRefresh" @refresherrestore="onRestore"
		 @refresherabort="onAbort" @scrolltolower="jjhseer">
		 <view class="pd pm20 pt20" v-if="isSearch">
		 	<view class="row">
		 		<view class="sdfsdtyxer pr col">
		 			<icon type="search" size="20" class="jjhhxerrt ab"></icon>
		 			<input type="text" v-model="seartext" class="sdftweert" placeholder=""  />
		 			<icon type="clear" class="jjhhxerrt ac" size="18" @tap="closert"></icon>
		 		</view>
		 		<view class="fz28 z3 pd pt10 " @tap="sjjheert">
		 			搜索
		 		</view>
		 	</view>
		 </view>
			<view v-if="SongList.length>0">
				
				<publiclist :SongList="SongList" v-if="SongList" @zhiding="zhiding" @delsd="delsd" @xuanze="xuanze" :isyhgg="isyhgg" :hggbbsd="hggbbsd"></publiclist>
				<uni-load-more :contentText="contentText" iconType="snow" :iconSize="36" :status="loading" v-if="SongList.length>19" />
				<view class="fz26 z9 cen pt20" v-if="SongList.length<20">
					------
				</view>
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
	import publiclist from "@/components/publiclist.vue"
	export default {
		props: ['SongTypeId', 'urls', 'isSearch', 'seartext', 'SearchType','isyhgg','hggbbsd'],
		data() {
			return {
				jhjhsde:0,
				sfgftyyd:true,
				chuci:false,
				isjihs:false,
				SongList: [],
				triggered: true,
				_freshing: false,
				pages: 1,
				loading: 'more',
				contentText: {
					contentdown: '------',
					contentrefresh: this.$store.state.lanser.Loading,
					contentnomore: '------'
				}
			}
		},
		components: {
			publiclist
		},
		computed: {
			kjhx() {
				return this.$store.state.lanser
			}
		},
		methods: {
			// 搜索
			closert() {
				this.seartext = ''
				this.$emit("closertr")
				this.sjjheert()
			},
			async kkjsdddv(a, b, c, d) {
				
				let sdeer = await this.post(a, b, c, d)
				this.jhjhsde = JSON.parse(sdeer.MessageContent).SongList.length
				JSON.parse(sdeer.MessageContent).SongList.map(a => {
					if (!a.IsSelected) {
						a.IsSelected = false
						a.cls = ""
					} else {
						a.cls = "act"
					}
					this.SongList.push(a)
				})
				this.$emit('huiojd',this.SongList.length)
				this.chuci = true
				this.isjihs= true
				this.sfgftyyd = true
				this.loading = "more"
			},
			initsd() {
				let hhgsd = {}
				hhgsd.Value = null
				if (this.urls == 'Search-Type') { // 分类
					hhgsd.SongTypeId = this.SongTypeId
				}
				if (this.urls == 'Search-Hot' || this.urls == 'Search-New' || this.urls == 'Search-Song') { // 热门 最新
					hhgsd.SongLangId = this.SongTypeId
				}
				hhgsd.PageNo = this.pages
				hhgsd.ListCount = 20
				hhgsd.Value = this.seartext
				hhgsd.SearchType = this.SearchType || 0
				this.kkjsdddv("vod/server/sendmessage", this.urls, hhgsd, 2)
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
			onRestore() {
				this.SongList = []
				this.triggered = 'restore'; // 需要重置
				this.pages = 1
				this.initsd()
				console.log("onRestore");
			},
			onAbort() {
				console.log("onAbort");
			},
			jjhseer(e) {
				if (this.SongList.length<20 ||this.jhjhsde<20){
					return
				}
				this.pages++
				this.loading = "loading"
				this.initsd()
			},
			// 置顶
			async zhiding(data) {
				await this.post("vod/server/sendmessage", "Song-Top", data.Id)
			},
			// 删除
			async delsd(data) {
				await this.post("vod/server/sendmessage", "Song-Remove", data.Id)
			},
			// 选择
			async xuanze(data) {
				await this.post("vod/server/sendmessage", "Song-Select", data.Id)
				uni.hideLoading()
			},
			sjjheert() { // 搜索觸發
			this.sfgftyyd = false
				this.pages = 1
				this.SongList = []
				this.initsd()
			}

		},
		mounted() {
			this.initsd()
		}
	}
</script>
<style scoped>

</style>
