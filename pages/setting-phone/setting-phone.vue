<template>
	<view>
		<image src="../../static/images/bg.jpg" class="p-fXY o6"></image>
		<view class="p-r">
			<view v-if="is_show">
				<image src="../../static/images/setupthe-icon.png" class="phone1"></image>
				
				<view class="w600 m-a bB-e1">
					<input type="text" v-model="submitData.phone" placeholder="请输入手机号" />
				</view>
				<view class="p-r w600 m-a bB-e1 flex1">
					<input type="text" v-model="submitData.code" placeholder="请输入验证码" />
					<view class="colorR font-w" style="z-index: 99;" @click="sendCode()" v-if="!hasSend">{{text}}</view>
					<view class="colorR font-w" style="z-index: 99;" v-if="hasSend">{{text}}</view>
				</view>
			
				<view class="btnAuto" @click="userInfoUpdate">完成</view>
			</view>
			
			<view v-else>
				<image src="../../static/images/setupthe-icon1.png" class="phone2"></image>
				<view class="text-center font-32">绑定手机号：{{userData.info&&userData.info.phone!=''?userData.info.phone:'暂未绑定'}}</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				is_show:true,
				userData:{},
				submitData:{
					phone:'',
					code:''
				},
				Router:this.$Router,
				Utils:this.$Utils,
				currentTime:61,
				text:'获取验证码',
				hasSend:false,
			}
		},
		
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getUserData'], self);
		},
		
		methods: {
			
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
			
			isShow(){
				const self = this;
				self.is_show = !self.is_show
			},
			
			userInfoUpdate(){
				const self = this;
				if(self.submitData.phone==''){
					self.$Utils.showToast('请填写手机号', 'none')
					return
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					phone:self.submitData.phone,
					name:self.submitData.name,
				};
				postData.smsAuth = {
					phone:self.submitData.phone,						
					code:self.submitData.code,
				};
				if(self.userData.info.behavior==0){
					postData.data.behavior = 1
				};
				postData.refreshToken = true;
				postData.saveAfter = [
					{
						tableName: 'Information',
						FuncName: 'update',
						searchItem:{
							user_no:uni.getStorageSync('user_info').user_no
						},
						data: {
							phone:self.submitData.phone
						},
					},
				];
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.navCurr = 1;
						self.$Utils.showToast('绑定成功', 'none');
						setTimeout(function() {
							self.getUserData();
							self.is_show = !self.is_show
						}, 1000);
						
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						if(self.userData.info.phone!=''){
							self.is_show = false
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

<style scoped>
.phone1{width: 138rpx;height: 222rpx;margin: 160rpx auto 70rpx;}
.phone2{width: 174rpx;height: 222rpx;margin: 160rpx auto 70rpx;}
.w600{width: 600rpx;}
input{margin: 10rpx auto 0;font-size: 26rpx;padding: 30rpx 0;max-width: 600rpx;flex: 1;}
.btnAuto{width: 600rpx;margin-top: 50rpx;font-weight: 800;}
</style>
