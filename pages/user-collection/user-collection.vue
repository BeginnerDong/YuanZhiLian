<template>
	<view class="p-3">
		
		<view class="line-h">
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
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.homeImg{width: 690rpx;height: 480rpx;}
.imgTxt{bottom: 0;background-image: linear-gradient(to bottom, rgba(0,0,0,0) 30%, rgba(0,0,0,0.3));padding: 20rpx 30rpx;width: 690rpx;box-sizing: border-box;}
</style>
