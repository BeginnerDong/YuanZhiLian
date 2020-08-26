<template>
	<view>
		
		<view class="head">
			<view class="flex colorf p-3">
				<image style="border-radius: 50%;overflow: hidden;" :src="userData.headImgUrl?userData.headImgUrl:''" class="wh100"></image>
				<view class="pl-2">
					<view class="font-w pb-1">{{userData.nickname?userData.nickname:''}}</view>
					<view class="sign" v-if="userData.info.behavior==0">游客</view>
					<view class="sign" v-if="userData.info.behavior==1">普通会员</view>
					<view class="sign" v-if="userData.info.behavior==2">黄金会员</view>
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
		
		<view v-show="navCurr==0&&userData.info&&userData.info.behavior==0">
			<view class="p-3 font-w bg-white">
				<view class="font-36">注册会员信息</view>
				
				<view class="bB-e1">
					<view class="pt-5">姓名</view>
					<input type="text" v-model="submitData.name" placeholder="请填写姓名" placeholder-style="color:#dedede" />
				</view>
				<view class="bB-e1">
					<view class="pt-5">手机号</view>
					<input type="text" v-model="submitData.phone" placeholder="请填写手机号" placeholder-style="color:#dedede" />
				</view>
				<view class="p-r bB-e1">
					<view class="pt-5">验证码</view>
					<input type="text" v-model="submitData.code" placeholder="请填写验证码" placeholder-style="color:#dedede" />
					<view class="colorR p-a mb-3 right-0 bottom-0 font-30" style="z-index: 99;" @click="sendCode()" v-if="!hasSend">{{text}}</view>
					<view class="colorR p-a mb-3 right-0 bottom-0 font-30" style="z-index: 99;" v-if="hasSend">{{text}}</view>
				</view>
				<view class="btnAuto" @click="userInfoUpdate">完成</view>
			</view>
		</view>
		
		
		<view v-show="navCurr==1">
			<view class="p-3 font-w bg-white mb-1">
				<view class="font-36 pb-3">黄金VIP会员</view>
				<view class="flex1">
					<view class="flex4 radius10 b-e1 p-r vipCard"
							:class="vipCurr==index?'on':''"
							v-for="(item,index) in productData" :key="index" 
							@click="vipChange(index)"
							v-if="index<3"
						>
						<view class="colorG font-34 flex">
							<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="kingIcon mr-1"></image>
							<view>{{item.title}}</view>
						</view>
						<view class="price1 font-50">{{item.price}}</view>
						<image src="../../static/images/vip-icon10.png" class="vipIcon" v-show="vipCurr==index"></image>
					</view>
				</view>
			</view>
			
			<view class="font-36 bg-white p-3 flex1">
				<image src="../../static/images/vip-icon12.png" class="wh48"></image>
				<view class="flex-1 pl-2">微信支付</view>
				<image src="../../static/images/vip-icon11.png" class="wh36"></image>
			</view>
			
			<view class="font-30 shadowM font-w flex1 pl-3 bg-white p-fX bottom-0">
				<view class="flex">总价：<text class="price1 font-40">{{productData[vipCurr]?productData[vipCurr].price:''}}</text></view>
				<view class="carBtn" @click="Utils.stopMultiClick(message)">确认支付</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navCurr:0,
				vipCurr:0,
				userData:{},
				submitData:{
					name:'',
					phone:'',
					code:''
				},
				Router:this.$Router,
				Utils:this.$Utils,
				currentTime:61,
				text:'获取验证码',
				hasSend:false,
				productData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getUserData','getProductData'], self);
		},
		
		methods: {
			
			message(){
				const self = this;
				 //self.goPay()
				uni.setStorageSync('canClick', false);
				wx.requestSubscribeMessage({
				  tmplIds: ['Ii3dbwsZGtoYj1OO0eAwxwzhPZsyjx_bXPiQpFFhBdU'],
				  success (res) { 
					  console.log(res)
					  if(res){
						  self.submit()
					  }
				  },
				  fail(err) {    //失败
				  					
				  	self.submit()
				  }
				})
			},
			
			submit(){
				const self = this;
				//uni.setStorageSync('canClick', false);
				var orderList = []
				var data = {
					type:1,
					level:1
				};
				orderList.push({product_id:self.productData[self.vipCurr].id,count:1,data:data})
				self.addOrder(orderList)
			},
			
			addOrder(orderList) {
				const self = this;	
				const postData = {}; 
				postData.orderList = self.$Utils.cloneForm(orderList);
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						self.goPay()
					} else {		
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};		
				};
				self.$apis.addOrder(postData, callback);
			},
			
			goPay() {
				const self = this;	
				const postData = {};
				postData.wxPay = {
					price:parseFloat(self.productData[self.vipCurr].price).toFixed(2),
				};
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				/* postData.payAfter = [
					{
						tableName: 'UserInfo',
						FuncName: 'update',
						searchItem:{
							user_no:uni.getStorageSync('user_info').user_no
						},
						data: {
							behavior:2,
							deadline:(self.userData.info.deadline==0?(new Date()).getTime() / 1000:self.userData.info.deadline)+self.productData[self.vipCurr].duration*86400
						},
					},
				]; */
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									self.$Utils.showToast('开通成功','none')
									setTimeout(function() {
										uni.navigateBack({
											delta:1
										})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									self.$Utils.showToast(res.msg,'none')
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							self.$Utils.showToast('开通成功','none')
							setTimeout(function() {
								uni.navigateBack({
									delta:1
								})
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(res.msg,'none')
					};
				};
				self.$apis.pay(postData, callback);
			},
			
			vipChange(index){
				const self = this;
				self.vipCurr = index
			},
			
			getProductData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2
				};
				postData.order = {
					duration:'asc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.productData = res.info.data;
					};
					uni.setStorageSync('canClick', true);
					self.$Utils.finishFunc('getProductData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			userInfoUpdate(){
				const self = this;
				if(self.submitData.name==''){
					self.$Utils.showToast('请填写姓名', 'none')
					return
				};
				if(self.submitData.phone==''){
					self.$Utils.showToast('请填写手机号', 'none')
					return
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					phone:self.submitData.phone,
					name:self.submitData.name,
					behavior:1
				};
				postData.smsAuth = {
					phone:self.submitData.phone,						
					code:self.submitData.code,
				};
				postData.refreshToken = true;
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.navCurr = 1;
						self.$Utils.showToast('完善成功', 'none');
						setTimeout(function() {
							self.getUserData();
						}, 1000);
						
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
			
			sendCode(){
				var self = this;
				if(self.hasSend){
					return;
				};
				var phone = self.submitData.phone;
				
				if (phone.trim().length != 11 || !/^1[3|4|5|6|7|8|9]\d{9}$/.test(phone)) {
					self.$Utils.showToast('请输入正确的手机号', 'none', 1000)
					return;
				}
				var postData = {
					data:{
						phone:self.submitData.phone,
					}
				};
				var callback = function(res){
					if(res.solely_code==100000){
						self.$Utils.showToast('发送成功', 'none', 1000)
						self.hasSend = true;
						var interval = setInterval(function() {
							self.currentTime--; //每执行一次让倒计时秒数减一
						
							self.text=self.currentTime + 's';//按钮文字变成倒计时对应秒数
							
							//如果当秒数小于等于0时 停止计时器 且按钮文字变成重新发送 且按钮变成可用状态 倒计时的秒数也要恢复成默认秒数 即让获取验证码的按钮恢复到初始化状态只改变按钮文字
							if (self.currentTime <= 0) {
								clearInterval(interval)
								self.hasSend = false;
								self.text='重新发送';
								self.currentTime= 61;
							}
						}, 1000);
					}else{
						self.$Utils.showToast('发送失败', 'none', 1000)
					};
				};
				self.$apis.codeGet(postData, callback);
			},
			
			change(type,i){
				const self = this;
				if(type == 'card'){
					self.cardCurr = i
				}else{
					if(i==0){
						if(self.userData.info.behavior==1){
							self.$Utils.showToast('您已经是普通会员', 'none', 1000);
							return
						}
					}
					self.navCurr = i
				}
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						if(self.userData.info.behavior==1){
							self.navCurr=1
						}
					};
					uni.setStorageSync('canClick', true);
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
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
