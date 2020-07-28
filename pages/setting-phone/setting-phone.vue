<template>
	<view>
		
		<view v-if="is_show">
			<image src="../../static/images/setupthe-icon.png" class="phone1"></image>
			
			<view class="w600 m-a bB-e1">
				<input type="text" value="" placeholder="请输入手机号" />
			</view>
			<view class="p-r w600 m-a bB-e1 flex1">
				<input type="text" value="" placeholder="请输入验证码" />
				<view class="colorR font-w">获取验证码</view>
			</view>
		
			<view class="btnAuto" @click="isShow">完成</view>
		</view>
		
		<view v-else>
			<image src="../../static/images/setupthe-icon1.png" class="phone2"></image>
			<view class="text-center font-32">绑定手机号：15689247539</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				is_show:true
			}
		},
		methods: {
			isShow(){
				const self = this;
				self.is_show = !self.is_show
			}
		}
	}
</script>

<style scoped>
.phone1{width: 138rpx;height: 222rpx;margin: 160rpx auto 70rpx;}
.phone2{width: 174rpx;height: 222rpx;margin: 160rpx auto 70rpx;}
.w600{width: 600rpx;}
input{margin: 10rpx auto 0;font-size: 26rpx;padding: 30rpx 0;max-width: 600rpx;flex: 1;}
.btnAuto{width: 600rpx;margin-top: 50rpx;font-weight: 800;}
</style>
