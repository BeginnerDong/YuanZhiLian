<template>
	<view>
		
		<view class="head p-r colorf">
			<image src="../../static/images/vip-img.png" class="p-aXY VipBg top-0"></image>
			<view class="px-3 p-r" >
				<view class="font-36 text-center tit" :style="{paddingTop:statusBar+'px'}">会员</view>
				
				<view class="p-r mt-3 colorV">
					<image src="../../static/images/vip-img1.png" class="VipImg"></image>
					<view class="p-aXY px-3 py-4 flex5">
						<view class="flex">
							<image src="../../static/images/vip-img2.png" class="wh100"></image>
							<view class="pl-2">
								<view class="font-w pb-1">柏拉图</view>
								<view class="sign">游客</view>
							</view>
						</view>
						<view class="flex1">
							<view class="font-26">开通会员，享受更多权益</view>
							<view class="grayBtn vipBtn font-w" @click="Router.navigateTo({route:{path:'/pages/VIP-opening/VIP-opening'}})">立即开通</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="font-36 font-w px-3 pt-5">专享特权</view>
		<view class="p-3 line-h flex1 flex-wrap">
			<view class="vipTQ flex mb-3">
				<image src="../../static/images/vip-icon.png" class="vipIcon"></image>
				<view>
					<view>海量信息</view>
					<view class="font-24 color6 mt-2">任性看</view>
				</view>
			</view>
		</view>
		
		
		
		
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/active/active'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>活动</view>
			</view>
			<view class="item on">
				<image src="../../static/images/nabar3-a.png" mode=""></image>
				<view>会员</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
		
		
	</view>
</template>

<script>
	const app = getApp()
	export default {
		data() {
			return {
				Router:this.$Router,
				statusBar: app.globalData.statusBar
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.VipBg{width: 100%;height: 400rpx;}
.head .tit{line-height: 100rpx;}
.VipImg{width: 690rpx;height: 310rpx;}
.colorV{color: #8B252A;}
.vipBtn{line-height: 66rpx;border-radius: 32rpx;width: 200rpx;background-image: linear-gradient(to right,#FEFBF6,#FFA6A9);color: #8B252A;}
.vipIcon{width: 99rpx;height: 109rpx;margin: 0 30rpx;}
.vipTQ{width: 330rpx;height: 160rpx;border-radius: 10rpx;background-color: #FAFAFA;}
</style>
