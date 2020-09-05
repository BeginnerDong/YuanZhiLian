<template>
	<view class="p-3">
		<image src="../../static/images/bg.jpg" class="p-fXY o6"></image>
		<view class="line-h p-r" v-for="(item,index) in mainData" :key="index"
		@click="toDetail(index)">
			<view class="p-r radius30 overflow-h shadowM">
				<image :src="item.bannerImg&&item.bannerImg[0]?item.bannerImg[0].url:''" class="homeImg"></image>
				<view class="colorf p-aX avoidOverflow imgTxt">{{item.introduce?item.introduce:''}}</view>
			</view>
			<view class="flex pt-2 pb-5">
				<image :src="item.gender==1?'../../static/images/home-icon5.png':'../../static/images/home-icon4.png'" class="wh32"></image>
				<view class="font-32 font-w pl-2 pr-3">{{item.nickname?item.nickname:''}}</view>
				<view class="color6">{{item.province?item.province:''}}·{{item.city?item.city:''}} {{item.age}}岁</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				Router:this.$Router,
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
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
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.noLoading = true;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
					};
				};
				self.$apis.userGet(postData, callback);
			},
			
			toDetail(index){
				const self = this;
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
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 2,
				};
				postData.getBefore = {
					log:{
						tableName:'Log',
						middleKey:'id',
						key:'relation_id',
						searchItem:{status:['in',[1]]},
						condition:'in'
					}
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
	}
</script>

<style scoped>
.homeImg{width: 690rpx;height: 480rpx;}
.imgTxt{bottom: 0;background-image: linear-gradient(to bottom, rgba(0,0,0,0) 30%, rgba(0,0,0,0.3));padding: 20rpx 30rpx;width: 690rpx;box-sizing: border-box;}
</style>
