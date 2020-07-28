<template>
	<view class="px-3 pt-3 font-26 color9">
		
		<view class="mb-3 bg-white radius10 p-3 flex1" @click="Router.navigateTo({route:{path:'/pages/active-detail/active-detail'}})">
			<image src="../../static/images/activity-img.png" class="activeImg"></image>
			<view class="activeTxt flex5">
				<view class="font-32 color2 mb-5 avoidOverflow2">西安市第四届全明星运动会</view>
				<view class="line-h t-indent20">
					<view class="mt-2 p-r actTime">2020年7月23日 14点</view>
					<view class="mt-3 p-r actDZ">西安市雁塔区高新大都荟</view>
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
			<view class="item on">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
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
	export default {
		data() {
			return {
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
.activeImg{width: 240rpx;height: 240rpx;border-radius: 10rpx;}
.activeTxt{width: 350rpx;height: 240rpx;}
.actTime::before,.actDZ::before{content: '';width: 10rpx;height: 10rpx;position: absolute;top: 50%;left: 0;margin-top: -5rpx;border-radius: 50%;}
.actTime::before{background-color: #38BD70;}
.actDZ::before{background-color: #FF515B;}
</style>
