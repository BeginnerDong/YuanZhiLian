<template>
	<view>
		<image src="../../static/images/bg.jpg" class="p-fXY o6"></image>
		<view class="p-r">
			<view class="font-26 color6 p-3 bg-white bB-e1">热点问题</view>
			<view class="px-3 bg-white">
				<view class="flex1 py-4 bB-f5" 
					v-for="(item,index) in mainData" :key="index"
					:data-id = "item.id"
					@click="Router.navigateTo({route:{path:'/pages/setting-answer/setting-answer?id='+$event.currentTarget.dataset.id}})"
				 >
					<view class="flex-1">{{item.title}}</view>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				
			</view>
			
			<button open-type="contact" style="position: fixed;bottom: 0;width: 100%;background-color: #fff;height: 100rpx;line-height: 100rpx;border-radius: 0;text-align: center;font-size: 15px;" class="d-flex a-center j-center">
				<image src="../../static/images/thepersonal-data-icon1.png" style="width: 30rpx;margin-right: 10rpx;height: 30rpx;"></image>
				没找到问题？咨询客服
			</button>
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
				};
				postData.getBefore = {
					article: {
						tableName: 'Label',
						middleKey: 'menu_id',
						key: 'id',
						searchItem: {
							title: ['in', ['帮助与反馈']],
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
</style>
