<template>
	<view class="px-3 pt-3 font-26 color9">
		<image src="../../static/images/bg.jpg" class="p-fXY o6"></image>
		
		<view class="mb-3 bg-white radius10 p-3 flex1 p-r" 
			v-for="(item,index) in mainData" :key="index"
			:data-id = "item.id"
			@click="Router.navigateTo({route:{path:'/pages/active-detail/active-detail?id='+$event.currentTarget.dataset.id}})"
		>
			<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="activeImg"></image>
			<view class="activeTxt flex5">
				<view class="font-32 color2 mb-5 avoidOverflow2">{{item.title?item.title:''}}</view>
				<view class="line-h t-indent20">
					<view class="mt-2 p-r actTime">{{item.small_title?item.small_title:''}}</view>
					<view class="mt-3 p-r actDZ">{{item.description?item.description:''}}</view>
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
			<view class="item on">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
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
	export default {
		
		data() {
			return {
				Router:this.$Router,
				mainData: [],
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
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
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
				postData.searchItem = {
					thirdapp_id: 2,
				}
				postData.getBefore = {
					article: {
						tableName: 'Label',
						middleKey: 'menu_id',
						key: 'id',
						searchItem: {
							title: ['in', ['活动']],
						},
						condition: 'in'
					}
				};
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data)
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
.activeImg{width: 240rpx;height: 240rpx;border-radius: 10rpx;}
.activeTxt{width: 350rpx;height: 240rpx;}
.actTime::before,.actDZ::before{content: '';width: 10rpx;height: 10rpx;position: absolute;top: 50%;left: 0;margin-top: -5rpx;border-radius: 50%;}
.actTime::before{background-color: #38BD70;}
.actDZ::before{background-color: #FF515B;}

.footer{left: 0;right: 0;}
</style>
