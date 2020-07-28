<template>
	<view>
		
		<view class="head p-r colorf">
			<image src="../../static/images/home-img.png" class="p-aXY homeBg top-0"></image>
			<view class="px-3 p-r" >
				<view class="font-36 text-center tit" :style="{paddingTop:statusBar+'px'}">缘之恋</view>
				<view class="d-flex a-center j-end" @click="isShow">
					<view>条件筛选</view>
					<image src="../../static/images/home-icon.png" class="sj-icon"></image>
				</view>
				
				<!-- banner -->
				<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#fff" class="banner">
					<swiper-item>
							<image src="../../static/images/home-banner.png" ></image>
					</swiper-item>
				</swiper>
			</view>
		</view>
		
		<!-- 金刚区 -->
		<view class="flex2 line-h py-4">
			<view class="font-26 flex4" @click="Router.navigateTo({route:{path:'/pages/aboutUS/aboutUS'}})">
				<image src="../../static/images/home-icon2.png" class="icon"></image>
				<view>关于我们</view>
			</view>
			<view class="font-26 flex4" @click="Router.navigateTo({route:{path:'/pages/safe/safe'}})">
				<image src="../../static/images/home-icon1.png" class="icon1"></image>
				<view>安全提示</view>
			</view>
			<view class="font-26 flex4" @click="Router.navigateTo({route:{path:'/pages/contactUS/contactUS'}})">
				<image src="../../static/images/home-icon3.png" class="icon2"></image>
				<view>联系我们</view>
			</view>
		</view>
		
		<!-- 信息展示 -->
		<view class="px-3 line-h" @click="Router.navigateTo({route:{path:'/pages/userDetail/userDetail'}})">
			<view class="p-r radius30 overflow-h shadowM">
				<image src="../../static/images/home-img1.png" class="homeImg"></image>
				<view class="colorf p-aX avoidOverflow imgTxt">喜欢就在一起，别辜负了相遇</view>
			</view>
			<view class="flex pt-2 pb-5">
				<image src="../../static/images/home-icon4.png" class="wh32"></image>
				<view class="font-32 font-w pl-2 pr-3">安静的夏日午后</view>
				<view class="color6">陕西·西安 22岁</view>
			</view>
		</view>
		
		<!-- 条件筛选 -->
		<view class="bg-mask z1000 line-h" v-show="is_show">
			<view class="p-aX bottom-0 radius20-T bg-white font-30 pt-3 flex5 choose">
				<view class="flex-1 flexY mx-3">
					<view>你想要寻找</view>
					<view class="flex2 pt-3 pb-5  px-5">
						<image src="../../static/images/home-icon6.png" class="wh120"></image>
						<image src="../../static/images/home-icon7.png" class="wh120"></image>
					</view>
					<view>你更倾向</view>
					<view class="flex mt-3 pb-5">
						<view class="btn-m160 Mbtn">西安</view>
						<view class="btn-m160">陕西</view>
						<view class="btn-m160">不限</view>
					</view>
					<view>你的标准</view>
					<view class="flex flex-wrap my-3">
						<view class="btn-m160 mb-2 Mbtn">博士</view>
						<view class="btn-m160 mb-2">硕士</view>
						<view class="btn-m160 mb-2">研究生</view>
						<view class="btn-m160 mb-2">本科</view>
						<view class="btn-m160 mb-2">专科</view>
						<view class="btn-m160 mb-2">高中</view>
						<view class="btn-m160 mb-2">不限</view>
					</view>
					<view>房、车标准</view>
					<view class="flex flex-wrap my-3">
						<view class="btn-m160 mb-2 Mbtn">有房有车</view>
						<view class="btn-m160 mb-2">有房没车</view>
						<view class="btn-m160 mb-2">没房有车</view>
						<view class="btn-m160 mb-2">没房没车</view>
						<view class="btn-m160 mb-2">不限</view>
					</view>
					<view class="flex1 mb-5">
						<view>年龄范围</view>
						<input type="text" value="" placeholder="输入你希望的年龄" />
					</view>
				</view>
				<view class="flex0 bg-white py-2 bT-f5">
					<view class="grayBtn mr-4">重置</view>
					<view class="grayBtn linearBtn ml-4" @click="isShow">确定</view>
				</view>
			</view>
		</view>
		
		
		
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/active/active'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>活动</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/VIP/VIP'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
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
	const app = getApp();
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
				statusBar: app.globalData.statusBar
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			isShow(){
				const self = this;
				self.is_show = !self.is_show
			}
		}
	};
</script>
<style scoped>
.homeBg{width: 100%;height: 400rpx;}
.head .tit{line-height: 100rpx;}
.banner,swiper-item{width: 690rpx;height: 320rpx;border-radius: 20rpx;overflow: hidden;margin-top: 10rpx;}
.icon{width: 68rpx;height: 68rpx;margin-bottom: 20rpx;}
.icon1{width: 52rpx;height: 62rpx;margin-bottom: 20rpx;}
.icon2{width: 64rpx;height: 56rpx;margin-bottom: 20rpx;}
.homeImg{width: 690rpx;height: 480rpx;}
.imgTxt{bottom: 0;background-image: linear-gradient(to bottom, rgba(0,0,0,0) 30%, rgba(0,0,0,0.3));padding: 20rpx 30rpx;width: 690rpx;box-sizing: border-box;}

.choose{height: 1100rpx;box-sizing: border-box;}

input{font-size: 30rpx;text-align: right;}
</style>
