<template>
	<view>
		
		<view class="head p-r colorf">
			<image src="../../static/images/details-img.png" class="p-aXY homeBg top-0"></image>
			<view class="p-r" >
				<view :style="{paddingTop:statusBar+'px'}" @click="Router.back({route:{path:-1}})">
					<image src="../../static/images/back.png" class="back"></image>
				</view>
				<view class="d-flex j-end a-center pr-3" @click="Utils.stopMultiClick(collect)">
					<image :src="mainData.log&&mainData.log.length>0&&mainData.log[0].status==1?'../../static/images/details-icon1.png':'../../static/images/details-icon.png'" class="wh30 mr-1"></image>
					<view>{{mainData.log&&mainData.log.length>0&&mainData.log[0].status==1?'已收藏':'收藏'}}</view>
				</view>
			</view>
		</view>
		
		<view class="content bg-white radius30-T px-3 p-r line-h">
			<view class="userImg p-a">
				<image style="border-radius: 50%;overflow: hidden;" :src="mainData.headImg&&mainData.headImg[0]?mainData.headImg[0].url:(mainData.gender==1?'../../static/images/home-icon7.png':'../../static/images/home-icon6.png')"></image>
			</view>
			<view class="font-38 font-w pt-5 flex">
				<view>{{mainData.nickname?mainData.nickname:'-'}}</view>
				<image :src="mainData.gender==1?'../../static/images/home-icon5.png':'../../static/images/home-icon4.png'" class="wh32 ml-2"></image>
			</view>
			<view class="color6 flex flex-wrap pb-2">
				<view class="pt-4 w-50">微信号：<text class="color2">{{mainData.wechat?mainData.wechat:'-'}}</text></view>
				<view class="pt-4 w-50">手机号：<text class="color2">{{mainData.phone?mainData.phone:'-'}}</text></view>
				<view class="pt-4 w-50">生日：<text class="color2">{{mainData.birthday?mainData.birthday:'-'}}</text></view>
				<view class="pt-4 w-50">星座：<text class="color2">{{mainData.constellation?mainData.constellation:'-'}}</text></view>
				<view class="pt-4 w-50">身高：<text class="color2">{{mainData.height?mainData.height:'-'}}</text></view>
				<view class="pt-4 w-50">体重：<text class="color2">{{mainData.weight?mainData.weight:'-'}}</text></view>
				<view class="pt-4 w-50">学历：<text class="color2">{{mainData.education?mainData.education:'-'}}</text></view>
				<view class="pt-4 w-50">籍贯：<text class="color2">{{mainData.origin?mainData.origin:'-'}}</text></view>
				<view class="pt-4 w-50">现居：<text class="color2">{{mainData.province?mainData.province:'-'}}·{{mainData.city?mainData.city:'-'}}</text></view>
				<view class="pt-4 w-50">婚姻：<text class="color2">{{mainData.marriage?mainData.marriage:'-'}}</text></view>
				<view class="pt-4 w-50">职业：<text class="color2">{{mainData.occupation?mainData.occupation:'-'}}</text></view>
				<view class="pt-4 w-50">月收入：<text class="color2">{{mainData.salary?mainData.salary:'-'}}</text></view>
				<view class="pt-4 w-50" v-if="mainData.car_house==1">房车：<text class="color2">有房有车</text></view>
				<view class="pt-4 w-50" v-if="mainData.car_house==2">房车：<text class="color2">有房无车</text></view>
				<view class="pt-4 w-50" v-if="mainData.car_house==3">房车：<text class="color2">有车无房</text></view>
				<view class="pt-4 w-50" v-if="mainData.car_house==4">房车：<text class="color2">无车无房</text></view>
				<view class="pt-4 w-50" v-if="!mainData.car_house">房车：<text class="color2">-</text></view>
			</view>
			
			<view class="font-32 font-w py-4">兴趣爱好</view>
			<view class="flex flex-wrap">
				<view class="tag" v-for="(item,index) in mainData.hobbyText" :key="index">{{item.title}}</view>
			</view>
			
			<view class="font-32 font-w py-4">个人介绍</view>
			<view class="line-h-md mb-2">
				{{mainData.introduce?mainData.introduce:'-'}}
			</view>
			
			<view class="font-32 font-w py-4">择偶标准</view>
			<view class="flex flex-wrap">
				<view class="tag" v-for="(item,index) in mainData.criteriaText" :key="index">{{item.title}}</view>
			</view>
			
			<view class="font-32 py-4 flex1">
				<view class="font-w">个人相册</view>
				<view class="color9 font-28">{{mainData.bannerImg&&mainData.bannerImg.length?mainData.bannerImg.length:0}}张</view>
			</view>
			<view class="flexX">
				<image v-for="(item,index) in mainData.bannerImg" :key="index" :src="item.url" class="img"></image>
			</view>
		</view>
		
		
		<view style="height: 160rpx;"></view>
		<view class="bg-white p-fX flex1 bottom-0  bT-e1 py-2 px-3">
			<button class="flex4 pl-2" open-type="contact">
				<image src="../../static/images/details-icon2.png" class="wh40 mb-1"></image>
				<view>联系客服</view>
			</button>
			<view class="btnAuto" @click="Router.navigateTo({route:{path:'/pages/VIP-opening/VIP-opening'}})">购买会员</view>
		</view>
		
		
	</view>
</template>

<script>
	const app = getApp();
	export default {
		data() {
			return {
				Router:this.$Router,
				statusBar: app.globalData.statusBar,
				mainData:{},
				Utils:this.$Utils,
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			
			
			collect() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if (self.mainData.log.length == 0) {
					self.addGoodLog()
				} else {
					self.updateGoodLog()
				};
			},
			
			addGoodLog() {
				const self = this;
				const postData = {};
				postData.data = {
					type: 1,
					title: '收藏成功',
					relation_id: self.mainData.id,
					user_no: uni.getStorageSync('user_info').user_no,
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.mainData.log.push({
							status: 1,
							id: res.info.id
						});
					} else {
						self.$Utils.showToast('收藏失败', 'none', 1000)
					};
					uni.setStorageSync('canClick', true);
				};
				self.$apis.logAdd(postData, callback);
			},
			
			
			updateGoodLog() {
				const self = this;
			
				const postData = {
					searchItem: {
						id: self.mainData.log[0].id
					},
					data: {
						status: -self.mainData.log[0].status
					}
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res.solely_code == 100000) {
						self.mainData.log[0].status = -self.mainData.log[0].status;
			
					} else {
						self.$Utils.showToast(res.msg, 'none', 1000)
					};
				};
				self.$apis.logUpdate(postData, callback);
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					thirdapp_id: 2,
					id:self.id
				};
				postData.getAfter = {
					hobbyText:{
						tableName:'Label',
						middleKey:'hobby',
						key:'id',
						searchItem:{
							status:1
						},
						condition:'in'
					},
					criteriaText:{
						tableName:'Label',
						middleKey:'criteria',
						key:'id',
						searchItem:{
							status:1
						},
						condition:'in'
					},
					log:{
						tableName:'Log',
						middleKey:'id',
						key:'relation_id',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						if(uni.getStorageSync('user_info').info.behavior==1){
							self.mainData.wechat = self.mainData.wechat.substr(0,2)+'***'+self.mainData.wechat.substr(5,self.mainData.wechat.length)
							self.mainData.phone = self.mainData.phone.substr(0,2)+'****'+self.mainData.phone.substr(6,self.mainData.phone.length)
						}
					};
					console.log(self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.informationGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
	button{border: 0;padding: 0;margin: 0;background: none;line-height: 1.5;font-size:12px}
	button:after{border: 0;}
.homeBg{width: 100%;height: 400rpx;}
.head .tit{line-height: 100rpx;}
.content{margin-top: 145rpx;}
.userImg{width: 170rpx;height: 170rpx;padding: 12rpx;border-radius: 50%;background-color: #fff;box-sizing: border-box;right: 50rpx;top: -85rpx;}
.img{width: 640rpx;height: 580rpx;border-radius: 20rpx;flex-shrink: 0;margin-right: 30rpx;}
.btnAuto{width: 520rpx;margin: 0;}
</style>
