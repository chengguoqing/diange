<template>
	<view class="">
		<view class=" pt20 pm20 btm row pd" v-for="(sd,idx) in SongList" :class="(hggbbsd==3&&idx==0)?'dsfsdt':''">
			<view class="fgfdtyyxe fz28 z6" v-if="isyhgg!=2">
				{{idx<10?'0'+(idx+1):(idx+1)}}
			</view>
			<view class="col">
				<view class="row">
					<view class="col">
						<view class="dian fz32 z3">
							{{sd.SongName}}
						</view>
						<view class="z9 fz24 mt10">
							{{sd.SingerName}}
						</view>
					</view>
					<view class="mt20" v-if="dsfrttyx">
						<view class="f_b" v-if="isyhgg!=2 && sd.IsSelected">
							<image src="../static/img/zhiding.png" class="cdftyxzer cz" mode="widthFix" @tap="jhhxdrer(idx)"></image>
							<image src="../static/img/sanchu.png" class="cdftyxzer  cz" mode="widthFix" @tap="hgsert(idx)"></image>

						</view>
						<view class="f_b" v-if="isyhgg!=1">
							<text class="kjjhxher cz" v-if="!sd.cls" @tap="kjhser(sd,1)">{{kjhx.Select}}</text>
							<!-- <text v-else class="kjjhxher cz ab" @tap="kjhser(sd,2)">{{kjhx.Selected}}</text> -->

						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		props: {
			isyhgg: { // 1隐藏点歌 2 搜索
				type: Number
			},
			SongList: {
				type: Array
			},
			dsfrttyx: {
				type: Boolean,
				default: true
			},
			hggbbsd: {
				type: String
			}
		},
		data() {
			return {
				jhgsee: [{
					name: '一年',
					gename: '华晨宇',
					cls: 'act'
				}, {
					name: '二年',
					gename: '华晨宇',
					cls: ''
				}, {
					name: '三年',
					gename: '华晨宇',
					cls: ''
				}, {
					name: '四年',
					gename: '华晨宇',
					cls: ''
				}, {
					name: '五年',
					gename: '华晨宇',
					cls: ''
				}]
			}
		},
		components: {

		},
		computed: {
			kjhx() {
				return this.$store.state.lanser
			}
		},
		methods: {
			async kjhser(sd, idx) {
				if (idx == 1) {
					await this.post("vod/server/sendmessage", "Song-Select", sd.Id)
					sd.IsSelected = true
					sd.cls = 'act'
				} else {
					// sd.cls=''
				}
			},
			async jhhxdrer(idx) {
				await this.post("vod/server/sendmessage", "Song-Top", this.SongList[idx].Id)
				let xcrtra = this.SongList[0],
					xcrtrb = this.SongList[idx]
				this.$set(this.SongList, idx, xcrtra)
				this.$set(this.SongList, 0, xcrtrb)
			},
			hihssd() {

			},
			hgsert(idx) {
				let th = this
				uni.showModal({
					content: this.$store.state.lanser.ConfirmDelete,
					cancelText: this.$store.state.lanser.Cancel,
					confirmText: this.$store.state.lanser.OK,
					async success(e) {
						if (e.confirm) {
							// 
							await th.post("vod/server/sendmessage", "Song-Remove", th.SongList[idx].Id)
							// 已选列表
							if (th.hggbbsd == 3) {
								th.SongList.splice(idx, 1)
							} else {
								th.SongList[idx].IsSelected = false
								th.SongList[idx].cls = ''
							}

						}
					}
				})
			}
		},
		mounted() {

		}
	}
</script>
<style scoped>
	.fgfdtyyxe {
		width: 70upx;
	}

	.fgfdtyyxe {
		line-height: 84upx;
	}

	.cdftyxzer {
		width: 44upx;
		margin-right: 40upx;
	}

	.kjjhxher {
		color: #FFD748;
		border: 1px solid #FFD748;
		display: inline-block;
		font-size: 26upx;
		padding: 4upx 20upx;
		border-radius: 20upx;
		width: 100upx;
		text-align: center;
	}

	.kjjhxher.ab {
		color: #AAAAAA;
		border-color: #AAAAAA;
	}

	.dsfsdt {
		background: #F8F8F8 !important;
	}

	.dsfsdt .cdftyxzer {
		opacity: 0.4;
		pointer-events: none
	}
</style>
