<template>
	<view>
		<image src="../../static/images/bg.jpg" class="p-fXY o6"></image>
		<view class="p-r">
			<view class="flex1 py-4 px-3 bg-white mb-2" @click="Router.navigateTo({route:{path:'/pages/setting-phone/setting-phone'}})">
				<view class="flex-1">手机号绑定</view>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			
			<view class="px-3 bg-white">
				<view class="flex1 py-4 bB-e1" @click="Router.navigateTo({route:{path:'/pages/setting-help/setting-help'}})">
					<view class="flex-1">帮助与反馈</view>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				<view class="flex1 py-4" @click="Router.navigateTo({route:{path:'/pages/setting-agreement/setting-agreement'}})">
					<view class="flex-1">用户协议</view>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
</style>
