<template>
	<view>
		<view class="font-26 color6 p-3 bg-white bB-e1">热点问题</view>
		<view class="px-3 bg-white">
			<view class="flex1 py-4 bB-f5" @click="Router.navigateTo({route:{path:'/pages/setting-answer/setting-answer'}})">
				<view class="flex-1">问题问题问题</view>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="flex1 py-4 bB-f5" @click="Router.navigateTo({route:{path:'/pages/setting-answer/setting-answer'}})">
				<view class="flex-1">问题问题问题</view>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
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
