<template>
	<view>
		
		<view class="flex p-3 pb-5 head">
			<view class="photo" style="overflow: hidden;border-radius: 50%;height: 120rpx;width: 120rpx;"><open-data type="userAvatarUrl"></open-data></view>
			<!-- <image src="../../static/images/vip-img2.png" class="wh120"></image> -->
			<view class="pl-2">
				<view class="font-w pb-2"><open-data type="userNickName"></open-data></view>
				<view class="tag linearBtn">普通会员</view>
			</view>
		</view>
		
		<view class="myList bg-white radius20 font-30 px-3 py-2">
			<view class="flex1 py-4" @click="Router.navigateTo({route:{path:'/pages/user-data/user-data'}})">
				<image src="../../static/images/my-icon3.png" class="wh33"></image>
				<view class="flex-1 px-2">个人资料</view>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="flex1 py-4" @click="Router.navigateTo({route:{path:'/pages/user-collection/user-collection'}})">
				<image src="../../static/images/my-icon2.png" class="wh36"></image>
				<view class="flex-1 px-2">我的收藏</view>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="flex1 py-4" @click="Router.navigateTo({route:{path:'/pages/setting/setting'}})">
				<image src="../../static/images/my-icon1.png" class="wh34"></image>
				<view class="flex-1 px-2">设置</view>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<button class="flex1 py-4" open-type="contact">
				<image src="../../static/images/my-icon.png" class="wh34"></image>
				<view class="flex-1 px-2">客服消息</view>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</button>
		</view>
		
		
		
		
		
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
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/VIP/VIP'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>会员</view>
			</view>
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar4-a.png" mode=""></image>
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

<style scoped>
	button{border: 0;margin: 0;background: none;line-height: 1.5;font-size: 15px;text-align: initial;}
	button:after{border: 0;}
.head{background-image: linear-gradient(to bottom,#FFC2C5,#F9DFE1);}
.tag{line-height: 40rpx;border-radius: 20rpx;min-width: auto;}
.myList{margin-top: -20rpx;}
</style>
