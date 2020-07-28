<template>
	<view class="px-5 py-4 infor">
		
		<view class="font-50 font-w py-2">填写你的个人信息</view>
		<view class="font-26 color6">让更多人的人认识你</view>
		
		<view class="mt-3 pt-3" contenteditable="true">昵称</view>
		<view class="p-r m-a bB-e1">
			<input type="text" value="" placeholder="请填写昵称" placeholder-style="font-size:26rpx;color:#999" />
		</view>
		<view class="mt-3 pt-3">微信号</view>
		<view class="p-r m-a bB-e1">
			<input type="text" value="" placeholder="请填写微信号" placeholder-style="font-size:26rpx;color:#999" />
		</view>
		<view class="mt-3 pt-3">手机号</view>
		<view class="p-r m-a bB-e1">
			<input type="text" value="" placeholder="请填写手机号" placeholder-style="font-size:26rpx;color:#999" />
		</view>
		<view class="mt-3 pt-3">生日</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="date"  @change="">
				<view class="font-26 color9 py-3 select">请选择生日日期</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">星座</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="selector" :range="constellation" @change="">
				<view class="font-26 color9 py-3 select">请选择星座</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">身高</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="selector" :range="height" @change="">
				<view class="font-26 color9 py-3 select">请选择身高</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">体重</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="selector" :range="weight" @change="">
				<view class="font-26 color9 py-3 select">请选择体重</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">学历</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="selector" :range="education" @change="">
				<view class="font-26 color9 py-3 select">请选择学历</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">籍贯</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="region"  @change="">
				<view class="font-26 color9 py-3 select">请选择籍贯</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">现居</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="region"  @change="">
				<view class="font-26 color9 py-3 select">请选择现居</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">婚姻状况</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="selector" :range="marry" @change="">
				<view class="font-26 color9 py-3 select">请选择婚姻状况</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">职业</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="selector" :range="work" @change="">
				<view class="font-26 color9 py-3 select">请选择职业</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">月收入</view>
		<view class="p-r m-a bB-e1 flex1">
			<picker mode="selector" :range="income" @change="">
				<view class="font-26 color9 py-3 select">请选择学历</view>
			</picker>
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">房车情况</view>
		<view class="p-r m-a bB-e1 flex1">
			<input type="text" value="" placeholder="请选择房车情况" placeholder-style="font-size:26rpx;color:#999" />
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">兴趣爱好</view>
		<view class="p-r m-a bB-e1 flex1" @click="isShow(1)">
			<input type="text" value="" placeholder="请填写兴趣爱好" placeholder-style="font-size:26rpx;color:#999" />
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">个人介绍</view>
		<view class="p-r m-a bB-e1">
			<!-- <input type="text" value="" placeholder="请输入个人介绍" /> -->
			<textarea value="" placeholder="请输入个人介绍" placeholder-style="font-size:26rpx;color:#999" />
		</view>
		<view class="mt-3 pt-3">择偶标准</view>
		<view class="p-r m-a bB-e1 flex1" @click="isShow(2)">
			<input type="text" value="" placeholder="请选择择偶标准" placeholder-style="font-size:26rpx;color:#999" />
			<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
		</view>
		<view class="mt-3 pt-3">相册(可传多张)</view>
		<view class="p-r m-a bB-e1 flex flex-wrap pt-4 pb-2 photo">
			<image src="../../static/images/thepersonaldata-icon1.png" class="wh210 mb-1"></image>
		</view>
		
		<view class="btnAuto">确定</view>
		
		
		<!-- 兴趣爱好 -->
		<view class="bg-mask" v-show="is_show==1">
			<view class="box radius20-T p-aX bottom-0 bg-white">
				<view class="flex1 p-3">
					<view @click="isShow(0)">取消</view>
					<view class="colorM" @click="isShow(0)">确定</view>
				</view>
				<view class="p-3 font-32 font-w">兴趣爱好</view>
				<view class="flex flex-wrap px-3">
					<view class="tag on">极限运动</view>
					<view class="tag">自驾游</view>
					<view class="tag on">宅</view>
					<view class="tag">绘画</view>
					<view class="tag on">电子游戏</view>
				</view>
			</view>
		</view>
		<!-- 择偶标准 -->
		<view class="bg-mask" v-show="is_show==2">
			<view class="box radius20-T p-aX bottom-0 bg-white">
				<view class="flex1 p-3">
					<view @click="isShow(0)">取消</view>
					<view class="colorM" @click="isShow(0)">确定</view>
				</view>
				<view class="p-3 font-32 font-w">择偶标准</view>
				<view class="flex flex-wrap px-3">
					<view class="tag">孝顺</view>
					<view class="tag">善良</view>
					<view class="tag on">温柔大方</view>
					<view class="tag on">气场一米八</view>
					<view class="tag">活泼开朗</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				constellation:['白羊座','金牛座','双子座','巨蟹座','狮子座','处女座','天秤座','天蝎座','射手座','摩羯座','水瓶座','双鱼座'],
				height:['160','170'],
				weight:['40kg以下','40~45kg','45~50kg','50~55kg','55~60kg','60kg以上'],
				education:['高中','专科','本科','研究生','硕士','博士','其他'],
				income:['5000以下','5000~8000','8000~10000','10000以上','其他'],
				marry:['未婚','离婚','其他'],
				work:['农民','司机','厨师','互联网','其他'],
				is_show:0
			}
		},
		methods: {
			isShow(i){
				const self = this;
				self.is_show = i
			}
		}
	}
</script>

<style scoped>
input{margin: 10rpx auto 0;font-size: 32rpx;padding: 30rpx 40rpx 30rpx 0;max-width: 100%;flex: 1;}
picker{width: 100%;z-index: 100;padding-right: 40rpx;box-sizing: border-box;}
.R-icon{position: absolute;right: 0;}
.wh210{width: 210rpx;height: 210rpx;margin-right: 10rpx;}
.photo image:nth-child(3n){margin-right: 0;}
.btnAuto{width: 650rpx;margin: 100rpx 0;font-weight: 800;}

.box{height: 700rpx;}
.tag{min-width: auto;padding: 0 20rpx;}
.box .on{background-color: #FF515B;color: #fff;}
.colorG{color: #1BCB97;}

textarea{margin: 40rpx auto;font-size: 32rpx;width: 100%;height: 200rpx;}
</style>
