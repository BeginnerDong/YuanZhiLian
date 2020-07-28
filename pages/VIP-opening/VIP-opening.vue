<template>
	<view>
		
		<view class="head">
			<view class="flex colorf p-3">
				<image src="../../static/images/vip-img2.png" class="wh100"></image>
				<view class="pl-2">
					<view class="font-w pb-1">柏拉图</view>
					<view class="sign">游客</view>
				</view>
			</view>
			<view class="font-32 p-r">
				<view class="p-a left-0 vipTit" @click="change('nav',0)" :class="navCurr==0?'colorf z10':'colorG'" >
					<image src="../../static/images/vip-icon1.png" class="iconBg" v-if="navCurr==0"></image>
					<image src="../../static/images/vip-icon6.png" class="iconBg" v-else></image>
					<view class="font-w flex0 p-aXY">
						<image src="../../static/images/vip-icon3.png" class="icon" v-if="navCurr==0"></image>
						<image src="../../static/images/vip-icon14.png" class="icon" v-else></image>
						<view>普通会员</view>
					</view>
				</view>
				<view class="p-a right-0 vipTit" @click="change('nav',1)" :class="navCurr==1?'colorf z10':'colorG'" >
					<image src="../../static/images/vip-icon5.png" class="iconBg" v-if="navCurr==1"></image>
					<image src="../../static/images/vip-icon2.png" class="iconBg" v-else></image>
					<view class="font-w flex0 p-aXY">
						<image src="../../static/images/vip-icon13.png" class="icon" v-if="navCurr==1"></image>
						<image src="../../static/images/vip-icon4.png" class="icon" v-else></image>
						<view>黄金会员</view>
					</view>
				</view>
			</view>
		</view>
		
		<view v-show="navCurr==0">
			<view class="p-3 font-w bg-white">
				<view class="font-36">注册会员信息</view>
				
				<view class="bB-e1">
					<view class="pt-5">姓名</view>
					<input type="text" value="" placeholder="请填写姓名" />
				</view>
				<view class="bB-e1">
					<view class="pt-5">手机号</view>
					<input type="text" value="" placeholder="请填写手机号" />
				</view>
				<view class="p-r bB-e1">
					<view class="pt-5">验证码</view>
					<input type="text" value="" placeholder="请填写验证码" />
					<view class="colorR p-a mb-3 right-0 bottom-0 font-30">获取验证码</view>
				</view>
				<view class="btnAuto">完成</view>
			</view>
		</view>
		
		
		<view v-show="navCurr==1">
			<view class="p-3 font-w bg-white mb-1">
				<view class="font-36 pb-3">黄金VIP会员</view>
				<view class="flex1">
					<view class="flex4 radius10 b-e1 p-r vipCard" @click="change('card',0)" :class="cardCurr==0?'onCard':''">
						<view class="colorG font-34 flex">
							<image src="../../static/images/vip-icon7.png" class="kingIcon mr-1"></image>
							<view>月卡</view>
						</view>
						<view class="price1 font-50">39</view>
						<image src="../../static/images/vip-icon10.png" class="vipIcon" v-show="cardCurr==0"></image>
					</view>
					<view class="flex4 radius10 b-e1 p-r vipCard" @click="change('card',1)" :class="cardCurr==1?'onCard':''">
						<view class="colorG font-34 flex">
							<image src="../../static/images/vip-icon8.png" class="kingIcon mr-1"></image>
							<view>季卡</view>
						</view>
						<view class="price1 font-50">39</view>
						<image src="../../static/images/vip-icon10.png" class="vipIcon" v-show="cardCurr==1"></image>
					</view>
					<view class="flex4 radius10 b-e1 p-r vipCard" @click="change('card',2)" :class="cardCurr==2?'onCard':''">
						<view class="colorG font-34 flex">
							<image src="../../static/images/vip-icon9.png" class="kingIcon mr-1"></image>
							<view>年卡</view>
						</view>
						<view class="price1 font-50">39</view>
						<image src="../../static/images/vip-icon10.png" class="vipIcon" v-show="cardCurr==2"></image>
					</view>
				</view>
			</view>
			
			<view class="font-36 bg-white p-3 flex1">
				<image src="../../static/images/vip-icon12.png" class="wh48"></image>
				<view class="flex-1 pl-2">微信支付</view>
				<image src="../../static/images/vip-icon11.png" class="wh36"></image>
			</view>
			
			<view class="font-30 shadowM font-w flex1 pl-3 bg-white p-fX bottom-0">
				<view class="flex">总价：<text class="price1 font-40">39</text></view>
				<view class="carBtn">确认支付</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navCurr:0,
				cardCurr:0
			}
		},
		methods: {
			change(type,i){
				const self = this;
				if(type == 'card'){
					self.cardCurr = i
				}else{
					self.navCurr = i
				}
			}
		}
	}
</script>
<style>
page{background-color: #f5f5f5}
</style>
<style scoped>
.head{background-color: #2E2E30;padding-bottom: 86rpx;}
.sign{color: #fff;background-color: #999;}
.vipTit{width: 395rpx;height: 86rpx;}
.icon{width: 35rpx;height: 31rpx;margin-right: 10rpx;}
.colorG{color: #7B7B7D;}
.kingIcon{width: 40rpx;height: 34rpx;}
.vipCard{width: 210rpx;height: 210rpx;}
.vipIcon{width: 71rpx;height: 61rpx;position: absolute;bottom: 0;right: 0;}
.onCard{border: 1px solid #FF515B;}

input{font-size: 30rpx;padding: 30rpx 0;line-height: 1;}
.btnAuto{width: 690rpx;margin: 50rpx 0 200rpx;}
</style>
