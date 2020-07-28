<template>
	<view>
		
		<view class="head p-r colorf">
			<image src="../../static/images/details-img.png" class="p-aXY homeBg top-0"></image>
			<view class="p-r" >
				<view :style="{paddingTop:statusBar+'px'}" @click="Router.back({route:{path:-1}})">
					<image src="../../static/images/back.png" class="back"></image>
				</view>
				<view class="d-flex j-end a-center pr-3">
					<image src="../../static/images/details-icon1.png" class="wh30 mr-1"></image>
					<view>收藏</view>
				</view>
			</view>
		</view>
		
		<view class="content bg-white radius30-T px-3 p-r line-h">
			<view class="userImg p-a">
				<image src="../../static/images/details-img1.png"></image>
			</view>
			<view class="font-38 font-w pt-5 flex">
				<view>安静的夏日午后</view>
				<image src="../../static/images/home-icon4.png" class="wh32 ml-2"></image>
			</view>
			<view class="color6 flex flex-wrap pb-2">
				<view class="pt-4 w-50">微信号：<text class="color2">ss****62</text></view>
				<view class="pt-4 w-50">手机号：<text class="color2">156****5689</text></view>
				<view class="pt-4 w-50">生日：<text class="color2">1995.05.06</text></view>
				<view class="pt-4 w-50">星座：<text class="color2">摩羯座</text></view>
				<view class="pt-4 w-50">身高：<text class="color2">170cm</text></view>
				<view class="pt-4 w-50">体重：<text class="color2">50Kg</text></view>
				<view class="pt-4 w-50">学历：<text class="color2">本科</text></view>
				<view class="pt-4 w-50">籍贯：<text class="color2">陕西·西安</text></view>
				<view class="pt-4 w-50">现居：<text class="color2">陕西·西安</text></view>
				<view class="pt-4 w-50">婚姻：<text class="color2">未婚</text></view>
				<view class="pt-4 w-50">职业：<text class="color2">工程师</text></view>
				<view class="pt-4 w-50">月收入：<text class="color2">10000</text></view>
				<view class="pt-4 w-50">房车：<text class="color2">有房有车</text></view>
			</view>
			
			<view class="font-32 font-w py-4">兴趣爱好</view>
			<view class="flex flex-wrap">
				<view class="tag">有责任心</view>
				<view class="tag">孝顺</view>
				<view class="tag">活泼开朗</view>
			</view>
			
			<view class="font-32 font-w py-4">个人介绍</view>
			<view class="line-h-md mb-2">
				开朗大方，喜欢认识新朋友，遇见新鲜事，探索新领域，如果你也对世界充满好奇心，那么，交个朋友吧
			</view>
			
			<view class="font-32 font-w py-4">择偶标准</view>
			<view class="flex flex-wrap">
				<view class="tag tag1">有责任心</view>
				<view class="tag tag2">孝顺</view>
				<view class="tag tag3">稳重</view>
			</view>
			
			<view class="font-32 py-4 flex1">
				<view class="font-w">个人相册</view>
				<view class="color9 font-28">5张</view>
			</view>
			<view class="flexX">
				<image src="../../static/images/details-img2.png" class="img"></image>
				<image src="../../static/images/details-img2.png" class="img"></image>
				<image src="../../static/images/details-img2.png" class="img"></image>
			</view>
		</view>
		
		
		<view style="height: 160rpx;"></view>
		<view class="bg-white p-fX flex1 bottom-0  bT-e1 py-2 px-3">
			<view class="flex4 pl-2">
				<image src="../../static/images/details-icon2.png" class="wh40 mb-1"></image>
				<view>联系客服</view>
			</view>
			<view class="btnAuto">购买会员</view>
		</view>
		
		
	</view>
</template>

<script>
	const app = getApp();
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
.homeBg{width: 100%;height: 400rpx;}
.head .tit{line-height: 100rpx;}
.content{margin-top: 145rpx;}
.userImg{width: 170rpx;height: 170rpx;padding: 16rpx;border-radius: 50%;background-color: #fff;box-sizing: border-box;right: 50rpx;top: -85rpx;}
.img{width: 640rpx;height: 580rpx;border-radius: 20rpx;flex-shrink: 0;margin-right: 30rpx;}
.btnAuto{width: 520rpx;margin: 0;}
</style>
