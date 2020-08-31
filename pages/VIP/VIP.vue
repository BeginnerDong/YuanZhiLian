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
							<image style="border-radius: 50%;overflow: hidden;"  :src="userData.headImgUrl?userData.headImgUrl:''" class="wh100"></image>
							<view class="pl-2">
								<view class="font-w pb-1">{{userData.nickname?userData.nickname:''}}</view>
								<view class="sign" v-if="userData.info.behavior==0">游客</view>
								<view class="sign" v-if="userData.info.behavior==1">普通会员</view>
								<view class="sign" v-if="userData.info.behavior==2">黄金会员</view>
							</view>
						</view>
						<view class="flex1">
							<view class="font-26" v-if="!isMember">开通黄金会员，享受更多权益</view>
							<view class="font-26" v-else>有效期至：{{Utils.timeto(userInfoData.deadline*1000,'ymd')}}</view>
							<view class="grayBtn vipBtn font-w" @click="Router.navigateTo({route:{path:'/pages/VIP-opening/VIP-opening'}})">{{isMember&&isMember==true?'立即续费':'立即开通'}}</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="font-36 font-w px-3 pt-5">专享特权</view>
		<view class="p-3 line-h flex1 flex-wrap">
			<view class="vipTQ flex mb-3" v-for="(item,index) in labelData" :key="index">
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="vipIcon"></image>
				<view>
					<view>{{item.title}}</view>
					<view class="font-24 color6 mt-2">{{item.description}}</view>
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
				statusBar: app.globalData.statusBar,
				userData:{},
				labelData:[],
				isMember:'',
				userInfoData:{},
				Utils:this.$Utils
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getLabelData'], self);
		},
		
		onShow() {
			const self = this;
			self.getUserData()
		},
		
		methods: {
			
			getLabelData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					parentid:15,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.labelData = res.info.data;
					};
					self.$Utils.finishFunc('getLabelData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getUserData() {
				const self = this;
				var nowTime = (new Date()).getTime() / 1000;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.noLoading = true;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						self.userInfoData = res.info.data[0].info;
						if(self.userInfoData.behavior>1){
							self.isMember = true;
						}else{
							self.isMember = false;
						}
					};
				};
				self.$apis.userGet(postData, callback);
			},
			
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
