<template>
	<view class="px-5 py-4 infor" v-if="showAll">
		<!-- <image src="../../static/images/bg.jpg" class="p-fXY o6"></image> -->
		<image src="../../static/images/bg.jpg" class="p-fXY o6"></image>
		<view class="p-r">
			<view class="font-50 font-w py-2">填写你的个人信息</view>
			<view class="font-26 color6">让更多人的人认识你</view>
			
			<view class="mt-3 pt-3" contenteditable="true">昵称</view>
			<view class="p-r m-a bB-e1">
				<input type="text" v-model="submitData.nickname" placeholder="请填写昵称" placeholder-style="font-size:26rpx;color:#999" />
			</view>
			<view class="mt-3 pt-3"><text style="color: red;">*</text>微信号</view>
			<view class="p-r m-a bB-e1">
				<input type="text" v-model="submitData.wechat" placeholder="请填写微信号" placeholder-style="font-size:26rpx;color:#999" />
			</view>
			<view class="mt-3 pt-3"><text style="color: red;">*</text>手机号</view>
			<view class="p-r m-a bB-e1">
				<input type="number" v-model="submitData.phone" placeholder="请填写手机号" placeholder-style="font-size:26rpx;color:#999" />
			</view>
			<view class="mt-3 pt-3"><text style="color: red;">*</text>身份证号</view>
			<view class="p-r m-a bB-e1">
				<input type="idcard" v-model="submitData.id_card" placeholder="请填写身份证号" placeholder-style="font-size:26rpx;color:#999" />
			</view>
			<view class="mt-3 pt-3">性别</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" :range="genderData"  @change="changeGender">
					<view class="font-26 color9 py-3 select" :style="genderData[genderIndex]?'font-size:32rpx;color:#222':''">{{genderData[genderIndex]?genderData[genderIndex]:'请选择性别'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">生日</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="date"  @change="birthdayChange">
					<view class="font-26 color9 py-3 select" :style="submitData.birthday!=''?'font-size:32rpx;color:#222':''">{{submitData.birthday!=''?submitData.birthday:'请选择生日日期'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">星座</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" :range="constellationData"  @change="Change" data-key="constellation">
					<view class="font-26 color9 py-3 select" :style="constellationData[constellationIndex]?'font-size:32rpx;color:#222':''">{{constellationData[constellationIndex]?constellationData[constellationIndex]:'请选择星座'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">身高</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" value="28" :range="heightData" @change="Change" data-key="height">
					<view class="font-26 color9 py-3 select" :style="heightData[heightIndex]?'font-size:32rpx;color:#222':''">{{heightData[heightIndex]?heightData[heightIndex]:'请选择身高'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">体重</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" value="28" :range="weightData" @change="Change" data-key="weight">
					<view class="font-26 color9 py-3 select" :style="weightData[weightIndex]?'font-size:32rpx;color:#222':''">{{weightData[weightIndex]?weightData[weightIndex]:'请选择体重'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">学历</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" :range="educationData"  @change="Change" data-key="education">
					<view class="font-26 color9 py-3 select" :style="educationData[educationIndex]?'font-size:32rpx;color:#222':''">{{educationData[educationIndex]?educationData[educationIndex]:'请选择学历'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">籍贯</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="region"  @change="hometownChange">
					<view class="font-26 color9 py-3 select" :style="submitData.origin!=''?'font-size:32rpx;color:#222':''">{{submitData.origin!=''?submitData.origin:'请选择籍贯'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">现居</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="region"  @change="addressChange">
					<view class="font-26 color9 py-3 select" :style="submitData.province!=''?'font-size:32rpx;color:#222':''">{{submitData.province!=''?submitData.province+'-'+submitData.city:'请选择现居地'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3"><text style="color: red;">*</text>婚姻状况</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker  mode="selector" :range="marriageData"  @change="Change" data-key="marriage">
					<view class="font-26 color9 py-3 select" :style="marriageData[marriageIndex]?'font-size:32rpx;color:#222':''">{{marriageData[marriageIndex]?marriageData[marriageIndex]:'请选择婚姻状况'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">职业</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" :range="occupationData"  @change="Change" data-key="occupation">
					<view class="font-26 color9 py-3 select" :style="occupationData[occupationIndex]?'font-size:32rpx;color:#222':''">{{occupationData[occupationIndex]?occupationData[occupationIndex]:'请选择职业'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">月收入</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" :range="salaryData"  @change="Change" data-key="salary">
					<view class="font-26 color9 py-3 select" :style="salaryData[salaryIndex]?'font-size:32rpx;color:#222':''">{{salaryData[salaryIndex]?salaryData[salaryIndex]:'请选择月收入'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<view class="mt-3 pt-3">房车情况</view>
			<view class="p-r m-a bB-e1 flex1">
				<picker mode="selector" :range="car_houseData"  @change="ChangecarHouse" range-key="title">
					<view class="font-26 color9 py-3 select" :style="car_houseData[car_houseIndex]?'font-size:32rpx;color:#222':''">{{car_houseData[car_houseIndex]?car_houseData[car_houseIndex].title:'请选择房车情况'}}</view>
				</picker>
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view>
			<!-- <view class="mt-3 pt-3">兴趣爱好</view>
			<view class="p-r m-a bB-e1 flex1" @click="isShow(1)">
				<input type="text" disabled="true" v-model="choosehobbyTitle" placeholder="请填写兴趣爱好" placeholder-style="font-size:26rpx;color:#999" />
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view> -->
			<view class="mt-3 pt-3">兴趣爱好</view>
			<view class="p-r m-a bB-e1">
				<!-- <input type="text" value="" placeholder="请输入个人介绍" /> -->
				<textarea v-model="submitData.hobby" placeholder="请输入兴趣爱好" placeholder-style="font-size:26rpx;color:#999" />
			</view>
			<view class="mt-3 pt-3">个人介绍</view>
			<view class="p-r m-a bB-e1">
				<!-- <input type="text" value="" placeholder="请输入个人介绍" /> -->
				<textarea v-model="submitData.introduce" placeholder="请输入个人介绍" placeholder-style="font-size:26rpx;color:#999" />
			</view>
			<view class="mt-3 pt-3">择偶标准</view>
			<view class="p-r m-a bB-e1 pdlr4" style="padding: 0 30rpx;">
				<view class="mt-3 pt-3"><text style="color: red;">*</text>年龄</view>
				<view class="p-r m-a bB-e1 flex1">
					<picker mode="selector"  :range="zo_ageData" @change="zoChange" data-key="zo_age">
						<view class="font-26 color9 py-3 select" 
						:style="zo_ageData[zo_ageIndex]?'color:#222':''">{{zo_ageData[zo_ageIndex]?zo_ageData[zo_ageIndex]:''}}</view>
					</picker>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				
				<view class="mt-3 pt-3"><text style="color: red;">*</text>身高</view>
				<view class="p-r m-a bB-e1 flex1">
					<picker mode="selector"  :range="zo_heightData" @change="zoChange" data-key="zo_height">
						<view class="font-26 color9 py-3 select" 
						:style="zo_heightData[zo_heightIndex]?'color:#222':''">{{zo_heightData[zo_heightIndex]?zo_heightData[zo_heightIndex]:''}}</view>
					</picker>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				
				<view class="mt-3 pt-3"><text style="color: red;">*</text>学历</view>
				<view class="p-r m-a bB-e1 flex1">
					<picker mode="selector"  :range="zo_educationData" @change="zoChange" data-key="zo_education">
						<view class="font-26 color9 py-3 select" 
						:style="zo_educationData[zo_educationIndex]?'color:#222':''">{{zo_educationData[zo_educationIndex]?zo_educationData[zo_educationIndex]:''}}</view>
					</picker>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				
				<view class="mt-3 pt-3"><text style="color: red;">*</text>地区</view>
				<view class="p-r m-a bB-e1 flex1">
					<picker mode="region"  @change="zohometownChange">
						<view class="font-26 color9 py-3 select" :style="submitData.zo_region!=''?'color:#222':''">{{submitData.zo_region!=''?submitData.zo_region:''}}</view>
					</picker>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				
				<view class="mt-3 pt-3"><text style="color: red;">*</text>职业</view>
				<view class="p-r m-a bB-e1 flex1">
					<picker mode="selector"  :range="zo_workData" @change="zoChange" data-key="zo_work">
						<view class="font-26 color9 py-3 select" 
						:style="zo_workData[zo_workIndex]?'color:#222':''">{{zo_workData[zo_workIndex]?zo_workData[zo_workIndex]:''}}</view>
					</picker>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				
				<view class="mt-3 pt-3"><text style="color: red;">*</text>车房</view>
				<view class="p-r m-a bB-e1 flex1">
					<picker mode="selector" :range="zo_car_houseData"  @change="zoChangecarHouse" range-key="title">
						<view class="font-26 color9 py-3 select" :style="zo_car_houseData[zo_car_houseIndex]?'color:#222':''">{{zo_car_houseData[zo_car_houseIndex]?zo_car_houseData[zo_car_houseIndex].title:''}}</view>
					</picker>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				
				<view class="mt-3 pt-3"><text style="color: red;">*</text>婚姻</view>
				<view class="p-r m-a bB-e1 flex1">
					<picker mode="selector"  :range="zo_marriageData" @change="zoChange" data-key="zo_marriage">
						<view class="font-26 color9 py-3 select" 
						:style="zo_marriageData[zo_marriageIndex]?'color:#222':''">{{zo_marriageData[zo_marriageIndex]?zo_marriageData[zo_marriageIndex]:''}}</view>
					</picker>
					<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
				</view>
				<!-- <input type="text" value="" placeholder="请输入个人介绍" /> -->
				<view class="mt-3 pt-3"><text style="color: red;">*</text>其他</view>
				<view class="p-r m-a bB-e1">
					<!-- <input type="text" value="" placeholder="请输入个人介绍" /> -->
					<textarea v-model="submitData.zo_other" placeholder="补充其他要求" placeholder-style="font-size:26rpx;color:#999" />
				</view>
			</view>
			<!-- <view class="p-r m-a bB-e1 flex1" @click="isShow(2)">
				<input type="text" disabled="true" v-model="choosecriteriaTitle" placeholder="请选择择偶标准" placeholder-style="font-size:26rpx;color:#999" />
				<image src="../../static/images/thepersonal-data-icon.png" class="R-icon"></image>
			</view> -->
			<view class="mt-3 pt-3">相册(可传多张)</view>
			<view class="p-r m-a bB-e1 flex flex-wrap pt-4 pb-2 photo">
				<image :src="item.url" v-for="(item,index) of submitData.bannerImg" :key="index" class="wh210 mb-1"></image>
				<image src="../../static/images/thepersonaldata-icon1.png" v-if="submitData.bannerImg.length<9" @click="upLoadImg('bannerImg')" class="wh210 mb-1"></image>
			</view>
			<!-- <view class="mt-3 pt-3" v-if="!isEdit"><text style="color: red;">*</text>验证码</view>
			<view class="p-r m-a bB-e1"  v-if="!isEdit">
				<input type="number" v-model="submitData.smsCode" placeholder="请填写验证码" placeholder-style="font-size:26rpx;color:#999" />
				<view class="colorR p-a mb-3 right-0 bottom-0 font-30" style="z-index: 99;" @click="sendCode()" v-if="!hasSend">{{text}}</view>
				<view class="colorR p-a mb-3 right-0 bottom-0 font-30" style="z-index: 99;" v-if="hasSend">{{text}}</view>
			</view> -->
			<view class="mt-3 pt-3">邀请码</view>
			<view class="p-r m-a bB-e1">
				<view v-if="hasCode">{{submitData.code}}</view>
				<input type="text"  v-if="!hasCode" v-model="submitData.code" placeholder="请填写邀请码(选填)" placeholder-style="font-size:26rpx;color:#999" />
			</view>
			<view class="btnAuto" @click="Utils.stopMultiClick(submit)">确定</view>
		</view>
		
		
		<!-- <cover-view class="bg-mask" v-show="is_show==1">
			<cover-view class="box radius20-T p-aX bottom-0 bg-white">
				<cover-view class="flex1 p-3">
					<cover-view @click="isShow(0)">取消</cover-view>
					<cover-view class="colorM" @click="isShow(0,'hobby')">确定</cover-view>
				</cover-view>
				<cover-view class="p-3 font-32 font-w">兴趣爱好</cover-view>
				<cover-view class="flex flex-wrap px-3">
					<cover-view class="tag" 
						v-for="(item,index) in hobbyData" 
						:key="index"
						:class="Utils.inArray(item.id,choosehobbyData)!=-1?'on':''"
						@click="chooseItem(index,'hobby')"
					>{{item.title}}</cover-view>
				</cover-view>
			</cover-view>
		</cover-view>
		<cover-view class="bg-mask" v-show="is_show==2">
			<cover-view class="box radius20-T p-aX bottom-0 bg-white">
				<cover-view class="flex1 p-3">
					<cover-view @click="isShow(0)">取消</cover-view>
					<cover-view class="colorM" @click="isShow(0,'criteria')">确定</cover-view>
				</cover-view>
				<cover-view class="p-3 font-32 font-w">择偶标准</cover-view>
				<cover-view class="flex flex-wrap px-3">
					<cover-view class="tag" 
						v-for="(item,index) in criteriaData" 
						:key="index"
						:class="Utils.inArray(item.id,choosecriteriaData)!=-1?'on':''"
						@click="chooseItem(index,'criteria')"
					>{{item.title}}</cover-view>
				</cover-view>
			</cover-view>
		</cover-view> -->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Utils:this.$Utils,
				submitData:{
					 wechat:'',   // 微信号 
					 phone:'',   // 手机号 
					 gender:'',   //性别:1.男;2.女 
					 nickname:'',   // 昵称 
					 province:'',   // 省 
					 city:'',   // 市 
					 education:'',   // 学历:1.高中2.专科3.本科4.研究生5.博士 
					 age:'',   // 年龄 
					 //listorder:'',   //自定义排序 
					 car_house:'',   // 1.有房有车2.有房无车3.有车无房4.无车无房 
					 introduce:'',   //个人介绍 
					 //headImg:[],   //头像 
					 //mainImg:[],   // 图片 
					 bannerImg:[],   // 相册 
					 birthday:'',   // 生日 
					 constellation:'',   // 星座 
					 height:'',   // 身高 
					 weight:'',   // 体重 
					 origin:'',   //籍贯 
					 live:'',   // 现居 
					 marriage:'',   // 婚姻状况 
					 occupation:'',   // 职业 
					 salary:'',   // 月收入 
					 hobby:'',   //爱好 
					 //criteria:'',   // 择偶标准 
					 is_show:1,
					 id_card:'',
					 
					 smsCode:'',
					 code:'',
					 zo_age:'不限',
					 zo_height:'不限',
					 zo_education:'不限',
					 zo_region:'不限',
					 zo_work:'不限',
					 zo_car_house:'0',
					 zo_marriage:'不限',
					 zo_other:''
				},
				is_show:0,
				
				constellationData:['白羊座','金牛座','双子座','巨蟹座','狮子座','处女座','天秤座','天蝎座','射手座','摩羯座','水瓶座','双鱼座'],
				constellationIndex:-1,
				heightData:[],
				heightIndex:-1,
				weightData:[],
				weightIndex:-1,
				educationData:['高中','专科','本科','研究生','硕士','博士','其他'],
				educationIndex:-1,
				marriageData:['未婚','离异未育','离异不带孩','离异有孩（男孩）','离异有孩（女孩）','丧偶未育','丧偶不带孩','丧偶有孩（男孩）','丧偶有孩（女孩）'],
				marriageIndex:-1,
				occupationData:['学生','销售','IT/互联网','通信/电子','生产/制造','物流/仓储','商贸/仓储','人事/行政',
				'高级管理','广告/市场','传媒/艺术','生物/制药','医疗/护理','金融','建筑/房地产','咨询/顾问','法律',
				'财会/审计','教育/科研','服务业','交通运输','政府机构','军人/警察','农林牧渔','自由职业','待业','其他'],
				occupationIndex:-1,
				salaryData:['2K-3K','3K-5K','5K-1W','1W以上'],
				salaryIndex:-1,
				car_houseData:[{title:'有车有房',value:1},{title:'有房无车',value:2},{title:'有车无房',value:3},{title:'无车无房',value:4}],
				genderData:['男','女'],
				genderIndex:-1,
				car_houseIndex:-1,
				hobbyData:[],
				choosehobbyData:[],
				choosehobbyTitle:'',
				criteriaData:[],
				choosecriteriaData:[],
				choosecriteriaTitle:'',
				currentTime:61,
				text:'获取验证码',
				hasSend:false,
				isEdit:false,
				hasCode:false,
				
				zo_ageData:['不限','18-25','25-30','30-35','35-40','40-45','45-50','50-55','55-60','60-65'],
				zo_ageIndex:0,
				zo_heightData:['不限'],
				zo_heightIndex:0,
				zo_educationData:['不限','高中','专科','本科','研究生','硕士','博士','其他'],
				zo_educationIndex:0,
				zo_workData:['不限','学生','销售','IT/互联网','通信/电子','生产/制造','物流/仓储','商贸/仓储','人事/行政',
				'高级管理','广告/市场','传媒/艺术','生物/制药','医疗/护理','金融','建筑/房地产','咨询/顾问','法律',
				'财会/审计','教育/科研','服务业','交通运输','政府机构','军人/警察','农林牧渔','自由职业','待业','其他'],
				zo_workIndex:0,
				zo_car_houseData:[{title:'不限',value:0},{title:'有车有房',value:1},{title:'有房无车',value:2},{title:'有车无房',value:3},{title:'无车无房',value:4}],
				zo_car_houseIndex:0,
				zo_marriageData:['不限','未婚','离异未育','离异不带孩','离异有孩（男孩）','离异有孩（女孩）','丧偶未育','丧偶不带孩','丧偶有孩（男孩）','丧偶有孩（女孩）'],
				zo_marriageIndex:0,
				showAll:false
			}
		},
		
		onLoad() {
			const self = this;
			/* for(var i=18;i<70;i++){
				self.zo_ageData.push(i);
			} */
			for(var i=140;i<221;i++){
				self.heightData.push(i+'cm');
				self.zo_heightData.push(i+'cm')
			}
			for(var i=40;i<100;i++){
				self.weightData.push(i+'kg');
			};
			//self.$Utils.loadAll(['getHobbyData','getCriteriaData'], self);
			if(self.heightData.length>0&&self.weightData.length){
				self.$Utils.loadAll(['getMainData'], self);
			}
			self.getCheckData()
		},
		
		onShow() {
			const self = this;
			self.getUserData()
		},
		
		methods: {
			
			getCheckData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:'会员权益'
				};
				postData.noLoading = true;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.checkData = res.info.data[0];
						if(self.checkData.listorder!=10){
							self.showAll = true
						}
					};
					self.$Utils.finishFunc('getCheckData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
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
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						if(self.mainData.phone!=''){
							self.isEdit = true
						};
						if(self.mainData.code!=''){
							self.hasCode = true
						};
						self.submitData.nickname = self.mainData.nickname;
						self.submitData.gender = self.mainData.gender;
						self.submitData.phone = self.mainData.phone;
						self.submitData.code = self.mainData.code;
						self.submitData.bannerImg = self.mainData.bannerImg;
						self.submitData.wechat = self.mainData.wechat;
						self.submitData.age = self.mainData.age;
						self.submitData.birthday = self.mainData.birthday;
						self.submitData.origin = self.mainData.origin;
						self.submitData.live = self.mainData.live;
						self.submitData.province = self.mainData.province;
						self.submitData.city = self.mainData.city;
						self.submitData.id_card = self.mainData.id_card;
						self.submitData.introduce = self.mainData.introduce;
						self.submitData.criteria = self.mainData.criteria;
						self.submitData.hobby = self.mainData.hobby;
						/* self.choosecriteriaData = self.mainData.criteria; */
						//self.choosehobbyData = self.mainData.hobby;
						self.genderIndex =parseInt(self.submitData.gender) - 1
						
						self.submitData.zo_age = self.mainData.zo_age;
						self.submitData.zo_height  = self.mainData.zo_height;
						self.submitData.zo_education  = self.mainData.zo_education;
						self.submitData.zo_region  = self.mainData.zo_region;
						self.submitData.zo_work  = self.mainData.zo_work;
						self.submitData.zo_car_house  = self.mainData.zo_car_house;
						self.submitData.zo_marriage = self.mainData.zo_marriage;
						self.submitData.zo_other = self.mainData.zo_other;
						/* var hobbyTitle = []
						for (var i = 0; i < self.hobbyData.length; i++) {
							for (var j = 0; j < self.submitData.hobby.length; j++) {
								if(self.hobbyData[i].id==self.submitData.hobby[j]){
									hobbyTitle.push(self.hobbyData[i].title)
								}
							}
						};
						self.choosehobbyTitle = hobbyTitle.join(',') */
						/* var criteriaTitle = []
						for (var i = 0; i < self.criteriaData.length; i++) {
							for (var j = 0; j < self.submitData.criteria.length; j++) {
								if(self.criteriaData[i].id==self.submitData.criteria[j]){
									criteriaTitle.push(self.criteriaData[i].title)
								}
							}
						};
						self.choosecriteriaTitle = criteriaTitle.join(',') */
						for (var i = 0; i < self.heightData.length; i++) {
							if(self.heightData[i]==self.mainData.height){
								self.heightIndex =i
								self.submitData.height = self.mainData.height
							}
						};
						for (var i = 0; i < self.constellationData.length; i++) {
							if(self.constellationData[i]==self.mainData.constellation){
								self.constellationIndex =i
								self.submitData.constellation = self.mainData.constellation
							}
						};
						for (var i = 0; i < self.weightData.length; i++) {
							if(self.weightData[i]==self.mainData.weight){
								self.weightIndex =i
								self.submitData.weight = self.mainData.weight
							}
						};
						for (var i = 0; i < self.occupationData.length; i++) {
							if(self.occupationData[i]==self.mainData.occupation){
								self.occupationIndex =i
								self.submitData.occupation = self.mainData.occupation
							}
						};
						
						
						for (var i = 0; i < self.educationData.length; i++) {
							if(self.educationData[i]==self.mainData.education){
								self.educationIndex =i
								self.submitData.education = self.mainData.education
							}
						};
						for (var i = 0; i < self.marriageData.length; i++) {
							if(self.marriageData[i]==self.mainData.marriage){
								self.marriageIndex =i
								self.submitData.marriage = self.mainData.marriage
							}
						};
						for (var i = 0; i < self.salaryData.length; i++) {
							if(self.salaryData[i]==self.mainData.salary){
								self.salaryIndex =i
								self.submitData.salary = self.mainData.salary
							}
						};
						for (var i = 0; i < self.car_houseData.length; i++) {
							if(self.car_houseData[i].value==self.mainData.car_house){
								self.car_houseIndex = i
								self.submitData.car_house = self.mainData.car_house
							}
						};
						
						for (var i = 0; i < self.zo_car_houseData.length; i++) {
							if(self.zo_car_houseData[i].value==self.mainData.zo_car_house){
								self.zo_car_houseIndex = i
								self.submitData.zo_car_house = self.mainData.zo_car_house
							}
						};
						
						for (var i = 0; i < self.zo_ageData.length; i++) {
							if(self.zo_ageData[i]==self.mainData.zo_age){
								self.zo_ageIndex =i
								self.submitData.zo_age = self.mainData.zo_age
							}
						};
						for (var i = 0; i < self.zo_heightData.length; i++) {
							if(self.zo_heightData[i]==self.mainData.zo_height){
								self.zo_heightIndex =i
								self.submitData.zo_height = self.mainData.zo_height
							}
						};
						for (var i = 0; i < self.zo_workData.length; i++) {
							if(self.zo_workData[i]==self.mainData.zo_work){
								self.zo_workIndex =i
								self.submitData.zo_work = self.mainData.zo_work
							}
						};
						
						
						for (var i = 0; i < self.zo_educationData.length; i++) {
							if(self.zo_educationData[i]==self.mainData.zo_education){
								self.zo_educationIndex =i
								self.submitData.zo_education = self.mainData.zo_education
							}
						};
						for (var i = 0; i < self.zo_marriageData.length; i++) {
							if(self.zo_marriageData[i]==self.mainData.zo_marriage){
								self.zo_marriageIndex =i
								self.submitData.zo_marriage = self.mainData.zo_marriage
							}
						};
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.informationGet(postData, callback);
			},
			
			upLoadImg(type) {
				const self = this;			
				
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						//self.submitData[type] = [];
						uni.hideLoading();
						self.submitData[type].push({url:res.info.url,type:'image'})
						console.log(self.submitData)
					} else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				uni.chooseImage({
					count: 9-self.submitData.bannerImg.length,
					success: function(res) {
						var tempFilePaths = res.tempFilePaths;
						for (var i = 0; i < tempFilePaths.length; i++) {
							var file = res.tempFiles[i];
							var obj = res.tempFiles[i].path.lastIndexOf(".");
							var ext = res.tempFiles[i].path.substr(obj+1);
							console.log(callback)
							self.$Utils.uploadFile(tempFilePaths[i], 'file', {
								tokenFuncName: 'getProjectToken',ext:ext,md5:'md5',totalSize:file.size,start:0,chunkSize:file.size,originName:'headImg'
							}, callback)
						}
					},
					fail: function(err) {
						uni.hideLoading();
					},			
				})			
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if(self.submitData.phone == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请填写手机号', 'none')
					return
				};
				if(self.submitData.wechat == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请填写微信号', 'none')
					return
				};
				if(self.submitData.id_card == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请填写身份证号', 'none')
					return
				};
				if(self.submitData.marriage == ''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请选择婚姻状况', 'none')
					return
				};
				if(self.submitData.bannerImg.length == 0){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请至少上传一张图片用于展示', 'none')
					return
				};
				if (self.submitData.phone.trim().length != 11 || !/^1[3|4|5|6|7|8|9]\d{9}$/.test(self.submitData.phone)) {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请输入正确的手机号', 'none', 1000)
					return;
				};
				self.informationUpdate();
				/* const pass = self.$Utils.checkComplete(self.submitData);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				
				if (pass) {	
					self.informationUpdate();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				}; */
			},
			
			informationUpdate(){
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				var newObject = self.$Utils.cloneForm(self.submitData);
				delete newObject.smsCode;
				postData.data = self.$Utils.cloneForm(newObject);
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				postData.saveAfter = [
					{
						tableName: 'UserInfo',
						FuncName: 'update',
						searchItem:{
							user_no:uni.getStorageSync('user_info').user_no
						},
						data: {
							phone:self.submitData.phone
						},
					},
				];
				if(self.userData.info.behavior==0){
					postData.saveAfter[0].data.behavior = 1
				};
				/* if(!self.isEdit){
					postData.smsAuth = {
						phone:self.submitData.phone,						
						code:self.submitData.smsCode,
					};
				}; */
				const callback = (res) => {
					if (res.solely_code==100000) {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('完善成功', 'none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.informationUpdate(postData, callback);
			},
			
			chooseItem(index,type) {
				const self = this;
				/* if((typeof str=='string')&&str.constructor==String){
					self['choose'+type+'Title'] = self['choose'+type+'Title'].join(',');
				}; */
				var position = self['choose'+type+'Data'].indexOf(self[type+'Data'][index].id);
				if (position >= 0) {
					self['choose'+type+'Data'].splice(position, 1);
					//self['choose'+type+'Title'].splice(position, 1);
				} else {
					self['choose'+type+'Data'].push(self[type+'Data'][index].id);
					//self['choose'+type+'Title'].push(self[type+'Data'][index].title);
				};
				console.log(self['choose'+type+'Data'])
			},
			
			getHobbyData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					parentid:8,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.hobbyData = res.info.data;
					};
					self.$Utils.finishFunc('getHobbyData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getCriteriaData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					parentid:9,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.criteriaData = res.info.data;
						self.getMainData()
					};
					self.$Utils.finishFunc('getCriteriaData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			
			isShow(i,type){
				const self = this;
				self.is_show = i;
				if(type){
					var titleArray = []
					self.submitData[type] = self['choose'+type+'Data'];
					for (var i = 0; i < self[type+'Data'].length; i++) {
						for (var j = 0; j < self.submitData[type].length; j++) {
							if(self[type+'Data'][i].id==self.submitData[type][j]){
								titleArray.push(self[type+'Data'][i].title)
							}
						}
					}
					console.log('titleArray',titleArray)
					self['choose'+type+'Title'] = titleArray.join(',');
				};
			},
			
			birthdayChange(e){
				const self = this;
				self.submitData.birthday = e.detail.value;
				self.submitData.age = new Date().getFullYear()-parseInt(self.submitData.birthday.split('-')[0])
				console.log(self.submitData);
			},
			
			addressChange(e){
				const self =  this;
				self.submitData.live = e.detail.value[0]+e.detail.value[1];
				self.submitData.province = e.detail.value[0];
				self.submitData.city  = e.detail.value[1];
				console.log(e);
			},
			
			Change(e){
				const self = this;
				self[e.currentTarget.dataset.key+'Index'] = e.detail.value;
				self.submitData[e.currentTarget.dataset.key] = self[e.currentTarget.dataset.key+'Data'][e.detail.value];
				console.log(self.submitData);
			},
			
			zoChange(e){
				const self = this;
				self[e.currentTarget.dataset.key+'Index'] = e.detail.value;
				self.submitData[e.currentTarget.dataset.key] = self[e.currentTarget.dataset.key+'Data'][e.detail.value];
				console.log(self.submitData);
			},
			
			ChangecarHouse(e){
				const self = this;
				self.car_houseIndex = e.detail.value;
				self.submitData.car_house = self.car_houseData[e.detail.value].value
			},
			
			zoChangecarHouse(e){
				const self = this;
				self.zo_car_houseIndex = e.detail.value;
				self.submitData.zo_car_house = self.zo_car_houseData[e.detail.value].value
			},
			
			changeGender(e){
				const self = this;
				self.genderIndex = e.detail.value;
				self.submitData.gender =parseInt(e.detail.value)+1;
				console.log(self.submitData);
			},
			
			hometownChange(e){
				const self =  this;
				self.submitData.origin = e.detail.value[0]+e.detail.value[1]+e.detail.value[2];
				console.log(e);
			},
			
			zohometownChange(e){
				const self =  this;
				self.submitData.zo_region = e.detail.value[0]+e.detail.value[1]+e.detail.value[2];
				console.log(e);
			},
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
