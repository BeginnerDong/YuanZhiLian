<template>
	<view>
		<image src="../../static/images/bg.jpg" class="p-fXY o6"></image>
		<view class="p-r">
			<view class="flex mx-3 py-3 bB-f5">
				<image src="../../static/images/contactus-icon.png" class="icon mr-3"></image>
				<view>{{mainData.phone?mainData.phone:''}}</view>
			</view>
			<view class="flex mx-3 py-3">
				<image src="../../static/images/contactus-icon1.png" class="icon1 mr-3"></image>
				<view>{{mainData.description?mainData.description:''}}</view>
			</view>
			<view class="f5Bj-H20"></view>
			
			<view class="p-3">
				<view class="content ql-editor" style="padding:0;" v-html="mainData.content">
				</view>
			</view>
		</view>
		
		
	</view>	
</template>

<script>
	const app = getApp();
	export default {
		data() {
			return {
				Router: this.$Router,
				mainData: {},
			}
		},

		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},

		methods: {

			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2
				};
				postData.getBefore = {
					article: {
						tableName: 'Label',
						middleKey: 'menu_id',
						key: 'id',
						searchItem: {
							title: ['in', ['联系我们']],
						},
						condition: 'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
					};
					console.log(self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style scoped>
.icon{width: 27rpx;height: 33rpx;}
.icon1{width: 28rpx;height: 33rpx;}
.map{width: 690rpx;height: 400rpx;}
</style>
