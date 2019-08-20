<template>
	<view class="content">
    <uni-nav-bar title="小工具" background-color="#ce1eec" color="#ffffff"
      @click-left="menuClick">
      <view slot="left" class="iconfont icon-caidan menu"></view>
    </uni-nav-bar>
    <uni-drawer :visible="drawerShow" @close="drawerClosed" class="uni-drawer-menu">
        <view style="padding:30upx;" v-for="(item, key) in menuOptions" :key="key" @click="drawerMenuClick(item)">
          <text :class="['iconfont', item.icon]" class="menu-text">{{item.text}}</text>
        </view>
    </uni-drawer>
    <!-- #ifdef H5-->
    <component :is="compContext"></component>
    <!-- #endif -->
	</view>
</template>

<script>
	import { uniNavBar, uniDrawer } from "@dcloudio/uni-ui"
  import img2base64 from '../img2base64/index.vue'
  import strLength from '../strLength/index.vue'
	export default {
		data() {
			return {
        drawerShow: false,
        menuOptions: [{
          text: '图片转base64',
          icon: 'icon-tupiantihuan',
          compName: 'img2base64'
        }, {
          text: '计算输入字符串长度',
          icon: 'icon-zifuchuanshujuji',
          compName: 'strLeng'
        }],
        compContext: 'strLength'
			}
		},
		onLoad() {

		},
		methods: {
      menuClick() {
        // 查看菜单
        this.drawerShow = true
      },
      drawerClosed() {
        // 关闭侧边栏
        this.drawerShow = false
      },
      drawerMenuClick(param) {
        console.log('param', param)
        // #ifdef H5
        this.compContext = param.compName
        // #endif
        this.drawerShow = false
      }
		},
		components: {
      uniNavBar,
      uniDrawer,
      img2base64,
      strLength
		}
	}
</script>

<style lang="scss">
.menu {
  padding-left: 5px;
}
 // #ifdef H5
.content /deep/ .uni-navbar .uni-navbar__header-btns:last-child {
    width: auto;
}
.uni-drawer-menu /deep/ .uni-drawer__content{
  background-color: #d94c66;
}
// #endif
// #ifndef H5
.content .uni-navbar .uni-navbar__header-btns:last-child {
    width: auto;
}
.uni-drawer-menu .uni-drawer__content{
  background-color: #d94c66;
}
// #endif
.menu-text {
  color: #FFFFFF;
  font-size: 24rpx;
}
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
