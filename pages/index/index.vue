<template>
	<view>
		
		<view class="head p-r colorf">
			<image src="../../static/images/home-img.png" class="p-aXY homeBg top-0"></image>
			<view class="px-3 p-r" >
				<view class="font-36 text-center tit" :style="{paddingTop:statusBar+'px'}">缘之恋</view>
				<view class="d-flex a-center j-end" @click="isShow">
					<view>条件筛选</view>
					<image src="../../static/images/home-icon.png" class="sj-icon"></image>
				</view>
				
				<!-- banner -->
				<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#fff" class="banner">
					<swiper-item v-for="(item,index) in sliderData" :key="index" @click="toActiveDetail(index)">
							<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" ></image>
					</swiper-item>
				</swiper>
			</view>
		</view>
		
		<!-- 金刚区 -->
		<view class="flex2 line-h py-4">
			<view class="font-26 flex4" @click="Router.navigateTo({route:{path:'/pages/aboutUS/aboutUS'}})">
				<image src="../../static/images/home-icon2.png" class="icon"></image>
				<view>关于我们</view>
			</view>
			<view class="font-26 flex4" @click="Router.navigateTo({route:{path:'/pages/safe/safe'}})">
				<image src="../../static/images/home-icon1.png" class="icon1"></image>
				<view>安全提示</view>
			</view>
			<view class="font-26 flex4" @click="Router.navigateTo({route:{path:'/pages/contactUS/contactUS'}})">
				<image src="../../static/images/home-icon3.png" class="icon2"></image>
				<view>联系我们</view>
			</view>
		</view>
		
		<!-- 信息展示 -->
		<view class="px-3 flex1 flex-wrap">
			<view class="line-h" v-for="(item,index) in mainData" :key="index"
			@click="toDetail(index)">
				<view class="p-r radius30 overflow-h shadowM infoImg">
					<image :src="item.bannerImg&&item.bannerImg[0]?item.bannerImg[0].url:''"></image>
					<view class="colorf p-aX avoidOverflow imgTxt">{{item.introduce?item.introduce:''}}</view>
				</view>
				<view class="flex pt-2 pb-2 w335">
					<image :src="item.gender==1?'../../static/images/home-icon5.png':'../../static/images/home-icon4.png'" class="wh32"></image>
					<view class="font-32 font-w pl-2 pr-3">{{item.nickname?item.nickname:''}}</view>
					
				</view>
				<view class="color6 avoidOverflow pb-5">{{item.province?item.province:''}}·{{item.city?item.city:''}} {{item.age}}岁</view>
			</view>
		</view>
		
		<!-- 条件筛选 -->
		<view class="bg-mask z1000 line-h" v-show="is_show">
			
			<view class="p-aX bottom-0 radius20-T bg-white font-30 pt-3 flex5 choose">
				<view style="position: absolute;top: 30rpx;right: 20rpx;color: #FF515B;font-weight: 700;" @click="closeSearch">取消</view>
				<view class="flex-1 flexY mx-3">
					<view>你想要寻找</view>
					<view class="flex2 pt-3 pb-5  px-5">
						<image @click="genderSearch(2)" :src="searchItem.gender&&searchItem.gender==2?'../../static/images/home-icon8.png':'../../static/images/home-icon6.png'" class="wh120"></image>
						<image @click="genderSearch(1)" :src="searchItem.gender&&searchItem.gender==1?'../../static/images/home-icon9.png':'../../static/images/home-icon7.png'" class="wh120"></image>
					</view>
					<view>你更倾向</view>
					<view class="flex mt-3 pb-5">
						<view class="btn-m160" @click="areaSearch('西安')" :class="searchItem.city&&searchItem.city=='西安'?'Mbtn':''">西安</view>
						<view class="btn-m160" @click="areaSearch('陕西')" :class="searchItem.province&&searchItem.province=='陕西'?'Mbtn':''">陕西</view>
						<view class="btn-m160" @click="areaSearch('不限')" :class="!searchItem.city&&!searchItem.province?'Mbtn':''">不限</view>
					</view>
					<view>你的标准</view>
					<view class="flex flex-wrap my-3">
						<view class="btn-m160 mb-2" @click="educationSearch('博士','search')" :class="searchItem.education&&searchItem.education=='博士'?'Mbtn':''">博士</view>
						<view class="btn-m160 mb-2" @click="educationSearch('硕士','search')" :class="searchItem.education&&searchItem.education=='硕士'?'Mbtn':''">硕士</view>
						<view class="btn-m160 mb-2" @click="educationSearch('研究生','search')" :class="searchItem.education&&searchItem.education=='研究生'?'Mbtn':''">研究生</view>
						<view class="btn-m160 mb-2" @click="educationSearch('本科','search')" :class="searchItem.education&&searchItem.education=='本科'?'Mbtn':''">本科</view>
						<view class="btn-m160 mb-2" @click="educationSearch('专科','search')" :class="searchItem.education&&searchItem.education=='专科'?'Mbtn':''">专科</view>
						<view class="btn-m160 mb-2" @click="educationSearch('高中','search')" :class="searchItem.education&&searchItem.education=='高中'?'Mbtn':''">高中</view>
						<view class="btn-m160 mb-2" @click="educationSearch('不限','delete')" :class="!searchItem.education?'Mbtn':''">不限</view>
					</view>
					<view>房、车标准</view>
					<view class="flex flex-wrap my-3">
						<view class="btn-m160 mb-2" @click="carSearch(1,'search')" :class="searchItem.car_house==1?'Mbtn':''">有房有车</view>
						<view class="btn-m160 mb-2" @click="carSearch(2,'search')" :class="searchItem.car_house==2?'Mbtn':''">有房没车</view>
						<view class="btn-m160 mb-2" @click="carSearch(3,'search')" :class="searchItem.car_house==3?'Mbtn':''">没房有车</view>
						<view class="btn-m160 mb-2" @click="carSearch(4,'search')" :class="searchItem.car_house==4?'Mbtn':''">没房没车</view>
						<view class="btn-m160 mb-2" @click="carSearch(5,'delete')" :class="!searchItem.car_house?'Mbtn':''">不限</view>
					</view>
					<view class="flex1 mb-5">
						<view>年龄范围</view>
						<!-- <input type="text" value="" placeholder="输入你希望的年龄" /> -->
						<picker mode="selector" :range="ageData"  @change="ageChange" range-key="title">
							<view class="font-26 color9 py-3 select" :style="ageData[ageIndex]?'font-size:32rpx;color:#222':''">
							{{ageData[ageIndex]?ageData[ageIndex].title:'请选择你希望的年龄'}}</view>
						</picker>
					</view>
				</view>
				<view class="flex0 bg-white py-2 bT-f5">
					<view class="grayBtn mr-4" @click="reset">重置</view>
					<view class="grayBtn linearBtn ml-4" @click="confirmSearch">确定</view>
				</view>
			</view>
		</view>
		
		<view class="bg-mask z1000 line-h" v-show="is_show1">
			<view class="p-aX bottom-0 radius20-T bg-white font-30 pt-3 flex5">
				<view class="text-center" style="font-weight: 700;font-size:18px">提示</view>
				<view class="text-center" style="padding:50rpx 0;">请同意授权使用小程序</view>
				<button class="flex0 bg-white py-2 bT-f5" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">
					<view class="grayBtn linearBtn">确定</view>
				</button>
			</view>
		</view>
		
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
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
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	import Vue from 'vue'
	const app = getApp();
	export default {
		data() {
			return {
				Utils:this.$Utils,
				Router:this.$Router,
				is_show: false,
				statusBar: app.globalData.statusBar,
				mainData:[],
				is_show1:false,
				sliderData:[],
				searchItem:{
					is_show:1,
					thirdapp_id:2
				},
				ageIndex:0,
				ageData:[{title:'不限',value:[1,1]},{title:'18-25',value:[18,25]},{title:'25-32',value:[25,32]},{title:'32-39',value:[32,39]}
				,{title:'39-45',value:[39,45]}]
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData','getSliderData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')&&!self.is_show1) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		onShow() {
			const self = this;
			self.getUserData()
		},
		
		methods: {
			
			ageChange(e){
				const self = this;
				self.ageIndex= e.detail.value;
				if(self.ageIndex==0){
					delete self.searchItem.age
				}else{
					self.searchItem.age = ['between',self.ageData[self.ageIndex].value]
				}
				self.searchItem = self.$Utils.cloneForm(self.searchItem)
			},
			
			closeSearch(){
				const self = this;
				self.searchItem = {
					is_show:1,
					thirdapp_id:2
				};
				self.is_show = false
			},
			
			reset(){
				const self = this;
				self.searchItem = {
					is_show:1,
					thirdapp_id:2
				}
			},
			
			confirmSearch(){
				const self = this;
				self.is_show = false
				self.getMainData(true)
			},
			
			genderSearch(type){
				const self = this;
				Vue.set(self.searchItem,'gender',type)
				//self.searchItem.gender = type
				self.searchItem = self.$Utils.cloneForm(self.searchItem)
			},
			
			areaSearch(area){
				const self = this;
				if(area=='西安'){
					//self.searchItem.city = '西安';
					Vue.set(self.searchItem,'city',area)
					if(self.searchItem.province){
						delete self.searchItem.province;
					}
				}else if(area=='陕西'){
					Vue.set(self.searchItem,'province',area)
					//self.searchItem.province = '陕西';
					if(self.searchItem.city){
						delete self.searchItem.city;
					}
				}else{
					delete self.searchItem.city;
					delete self.searchItem.province;
				}	
				self.searchItem = self.$Utils.cloneForm(self.searchItem)
			},
			
			educationSearch(text,type){
				const self = this;
				console.log(type)
				if(type=='search'){
					Vue.set(self.searchItem,'education',text)
					//self.searchItem.education = text
				}else if(type=='delete'){
					delete self.searchItem.education
				}
				console.log(self.searchItem)
				self.searchItem = self.$Utils.cloneForm(self.searchItem)
			},
			
			carSearch(num,type){
				const self = this;
				if(type=='search'){
					Vue.set(self.searchItem,'car_house',num)
					//self.searchItem.car_house = num
				}else if(type=='delete'){
					delete self.searchItem.car_house
				}
				console.log(self.searchItem)
				self.searchItem = self.$Utils.cloneForm(self.searchItem)
			},
			
			toActiveDetail(index){
				const self = this;
				if(self.sliderData[index].passage1!=''){
					self.Router.navigateTo({route:{path:'/pages/active-detail/active-detail?id='+self.sliderData[index].passage1}})
				}
			},
			
			getSliderData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					menu_id:2
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.sliderData = res.info.data
					};
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			toDetail(index){
				const self = this;
				
				if(self.userData.information[0].phone==''){
					uni.showModal({
						title:'提示',
						content:'完善您的个人资料即可查看，是否立即完善',
						confirmColor:'#FF515B',
						success(res) {
							if(res.confirm){
								self.Router.navigateTo({route:{path:'/pages/user-data/user-data'}})
							}
						}
					})
					return
				};
				if(self.userData.info.behavior==0){
					uni.showModal({
						title:'提示',
						content:'填写信息成为普通会员即可查看，是否立即填写',
						confirmColor:'#FF515B',
						success(res) {
							if(res.confirm){
								self.Router.navigateTo({route:{path:'/pages/VIP-opening/VIP-opening'}})
							}
						}
					})
				}else{
					self.Router.navigateTo({route:{path:'/pages/userDetail/userDetail?id='+self.mainData[index].id}})
				}
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);	
				const callback = (user, res) => {
					console.log(res)
					self.informationUpdate(user);
				};
				self.$Utils.getAuthSetting(callback);
			},
			
			informationUpdate(user){
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					nickname:user.nickname,
					headImg:[{type:'img',url:user.avatarUrl}],
				};
				postData.searchItem = {
					user_no:self.userData.user_no
				};
				postData.refreshToken = true;
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.is_show1 = false;
						self.$Utils.showToast('授权成功', 'none');
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.informationUpdate(postData, callback);
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.noLoading = true;
				postData.getAfter = {
					information:{
						tableName:'Information',
						middleKey:'user_no',
						key:'user_no',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						if(self.userData.headImgUrl == ''){
							self.is_show1 = true
						}
					};
				};
				self.$apis.userGet(postData, callback);
			},
			
			isShow(){
				const self = this;
				self.is_show = !self.is_show
			},
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 10
					}
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem)
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data)
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.informationGet(postData, callback);
			},
		}
	};
</script>
<style scoped>
.homeBg{width: 100%;height: 400rpx;}
.head .tit{line-height: 100rpx;}
.banner,swiper-item{width: 690rpx;height: 320rpx;border-radius: 20rpx;overflow: hidden;margin-top: 10rpx;}
.icon{width: 68rpx;height: 68rpx;margin-bottom: 20rpx;}
.icon1{width: 52rpx;height: 62rpx;margin-bottom: 20rpx;}
.icon2{width: 64rpx;height: 56rpx;margin-bottom: 20rpx;}
.infoImg{width: 335rpx;height: 280rpx;}
.infoImg image{width: 100%;height: 100%;}
.imgTxt{bottom: 0;background-image: linear-gradient(to bottom, rgba(0,0,0,0) 30%, rgba(0,0,0,0.3));padding: 20rpx 30rpx;width: 335rpx;box-sizing: border-box;}
.w335{width: 335rpx;}

.choose{height: 1100rpx;box-sizing: border-box;}

input{font-size: 30rpx;text-align: right;}
</style>
