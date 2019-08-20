<template>
	<view class="content">
		<view class="upfile">
			<text class="iconfont icon-dakai upfile-text" @click="openfile" v-if="imgUrl.length===0">打开文件</text>
			<image :src="imgUrl" mode="scaleToFill" v-else class="img-yl"></image>
		</view>
		<view class="btn-area">
			<button type="primary" size="mini" class="img2base64" @click="img2baseClick" :loading="img2baseLoad">转换图片</button>
		</view>
		<view class="base-str">
			<text style="word-wrap:break-word">{{imgbaseStr}}</text>
		</view>
		<uni-popup ref="popup" type="center">
			请选择转换的图片
		</uni-popup>
	</view>
</template>

<script>
	import { uniPopup } from "@dcloudio/uni-ui"
	export default {
		data() {
			return {
				imgbaseStr: '',
				img2baseLoad: false,
				imgUrl: ''
			}
		},
		onLoad() {

		},
		methods: {
			openfile() {
				uni.chooseImage({
					count: 2,
					sourceType: ['album', 'camera'],
					success: (res) => {
						this.imgUrl = res.tempFilePaths[0]
					}
				})
			},
			img2baseClick() {
				let self = this
				if (!this.imgUrl) {
					this.$refs.popup.open()
					return false
				}
				this.img2baseLoad = true
				uni.getImageInfo({
					src: this.imgUrl,
					success: (res) => {
						// H5端使用代码
						// #ifdef H5
						let img = new Image()
						img.src = res.path
						img.onload = function () {
							self.imgbaseStr = self.ImageToCanvas(img)
							self.img2baseLoad = false
						}
						// #endif
						// 微信端使用代码
						// #ifdef MP-WEIXIN
						let fileType = res.type
						wx.getFileSystemManager().readFile({
							filePath: res.path,
							encoding: 'base64',
							success: res => {
								this.img2baseLoad = false
								let base64 = `data:image/${fileType};base64,` + res.data 
								self.imgbaseStr = base64
							}, fail: err => {
								this.img2baseLoad = false
								console.log(err);
							}
						})
						// #endif
					}
				})
			},
			ImageToCanvas(image) {
				var canvas = document.createElement("canvas")
				canvas.width = image.width
				canvas.height = image.height
				canvas.getContext("2d").drawImage(image, 0, 0)
				return canvas.toDataURL()
			}
		},
		components: {
			uniPopup
		}
	}
</script>

<style lang="scss">
.upfile {
	width: 500rpx;
	height: 250rpx;
	border: 2rpx #C8C7CC dashed;
	margin: 10rpx auto;
	display: flex;
	justify-content: center;
	align-items: center;
	.upfile-text {
		color: $uni-text-color;
	}
	.img-yl {
		width: 100%;
		height: 100%;
	}
}
.btn-area {
	padding: 10rpx 0rpx;
	text-align: center;
}
.base-str {
	width: 500rpx;
	min-height: 250rpx;
	border: 2rpx #C8C7CC dashed;
	margin: 10rpx auto;
}
</style>
