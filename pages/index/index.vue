<template>
	<view>
		<view class="zhanwei"></view>
		<!--搜索框开始-->
		<view class="cu-bar search bg-gradual-orange">
			<view class="search-form round">
				<text class="cuIcon-search"></text>
				<input v-model="search" placeholder="请输入你想要的商品" />
			</view>
			<view class="action">
				<text class="cuIcon-scan" style="font-size: 150%;"></text>
			</view>
		</view>
		<!--搜索框结束-->
		<!--Tab开始-->
		<view>
			<scroll-view class="nav bg-white" scroll-x>
				<view class="flex text-center">
					<view :class="thistab==index?'text-orange cur':''" @click="qiehuan(index)" v-for="(item,index) in TabLists" :key="index"
					 class="cu-item flex-sub">
						{{item}}
					</view>
				</view>
			</scroll-view>
		</view>
		<!--Tab结束-->
		<!--轮播开始-->
		<swiper style="height: 250upx;margin-top: 5upx;" class="square-dot" :circular="true" :indicator-dots="true">
			<swiper-item v-for="(item,index) in banners" :key="index">
				<image mode="scaleToFill" class="swiperimg" :src="item.url"></image>
			</swiper-item>
		</swiper>
		<!--轮播结束-->
		<!--进入众筹开始-->
		<view class="bg-white zhongchou">
			<view style="display: flex;align-items: center;">
				<image style="width: 50upx;height: 50upx;margin-right: 5upx;" src="../../static/tab/cart.png"></image>
				<text style="font-weight: bold;font-size: 110%;">来众筹</text>
			</view>
			<view class="text-gray">查看全部<text class="cuIcon-right"></text></view>
		</view>
		<!--进入众筹结束-->
		<!--导航图标开始-->
		<view class="icon-father bg-white">
			<view v-for="(item,index) in iconLists" :key="index" class="icon-item">
				<image :src="item.url"></image>
				<view style="text-align: center;">{{item.name}}</view>
			</view>
		</view>
		<!--导航图标结束-->
		<!--特价商品开始-->
		<view style="padding-top: 30upx;" class="tejia bg-white">
			<!--bar开始-->
			<view class="flex align-center justify-between tejiabar">
				<view class="flex align-center">
					<view>
						<image style="width: 60upx;height: 60upx;" src="../../static/icon/qian.png"></image>
					</view> 
					<view style="font-size: 130%;" class="text-bold">百亿补贴</view>
					<view style="margin-left: 10upx;" class="text-bold cu-tag">大牌正品 官方补贴</view>
				</view>
				<view class="text-gray">
					全部<text class="cuIcon-right"></text>
				</view>
			</view>
			<!--bar结束-->
			<!--商品列表开始-->
			<view style="padding: 20upx 20upx 20upx 20upx;" class=" flex justify-around">
				<view v-for="(item,index) in tejiaLists" :key="index">
					<view style="position: relative;" class="flex justify-center">
						<image class="image1" :src="item.url"></image>
						<view style="position: absolute;bottom: 10upx;" class="cu-tag sm bg-red">{{item.tag}}</view>
					</view>
					<view style="color: red;text-align: center;">
						<text style="font-size: 80%;">￥</text> {{item.price}}
					</view>
				</view>
			</view>
			<!--商品列表结束-->
		</view>
		<!--特价商品结束-->
		<!--商品列表-->
		<view style="margin-top: 30upx;">
			<view style="padding: 20upx 20upx 20upx 20upx;" class="flex justify-around bg-white" v-for="(p,i) in goodsLists" :key="i">
				<view style="width:250upx">
					<image style="width: 250upx;height: 250upx;" :src="p.url"></image>
				</view>
				<view style="width:400upx;flex-direction: column;border-bottom: 0.5upx solid #e7e7e7;" class="flex justify-between">
					<view>
						<view style="font-weight: bold;font-size: 30upx;">
							<text v-if="p.tag1==true" class="cu-tag sm bg-gradual-orange round">女神节</text> {{p.title}}
						</view>
						<view class="cu-tag sm bg-brown radius">{{p.shop}}</view>
					</view>
					<view>
						<view style="margin-bottom: 20upx;">
							<text v-if="p.tag2==true" class="cu-tag sm bg-red radius">小编推荐</text>
							<text v-if="p.tag3" class="cu-tag sm bg-orange radius">假一赔十</text>
						</view>
						<view style="font-size: 120%;">
							<text style="color: red;font-size: 120%;"><text style="font-size: 70%;">￥</text>{{p.price}}</text>
							<text style="color: grey;font-size: 90%;">已买{{p.num}}+</text>
						</view>
						<view style="width:100%;height: 10upx;"></view>
					</view>
				</view>
			</view>
		</view>
		<!--商品列表结束-->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				shu: null,
				search: "",
				TabLists: ["热门", "水果", "蔬菜", "肉类", "众筹"],
				thistab: 0,
				banners: [],
				iconLists: [],
				tejiaLists:[],
				goodsLists:[]
			}
		},
		onLoad() {
			this.getbanners();
			this.geticonLists();
			this.gettejia();
			this.getgoodsLists();
			// var carts=this.$store.state.carts;
			// this.upPushId();
		},
		onReady() {

		},
		methods: {
			upPushId(){
				var uid=uni.getStorageSync("uid");
				var cinfo=plus.push.getClientInfo();
				if(uid){
					uni.request({
						url:this.$url+"/info/uppushid",
						method:"POST",
						data:{
							uid:uid,
							pid:cinfo.clientid
						},
						success: (res) => {
							console.log(res.data);					
						}
					})
				}
			},
			qiehuan(index) {
				this.thistab = index;
			},
			//获得轮播图的数据
			getbanners() {
				var data = [{
					url: "https://m.360buyimg.com/babel/jfs/t1/177085/8/10690/115690/60d29c55E244614a7/97c95689186258c0.png",
					action: ""
				}, {
					url: "https://m.360buyimg.com/babel/jfs/t1/177515/16/10771/191566/60d2a90fE111f5869/9dd3a39c10fb49cd.png",
					action: ""
				}, {
					url: "https://m.360buyimg.com/babel/jfs/t1/192820/22/9531/172830/60d155b8E813558ed/ac953ce69a1b4312.png",
					action: ""
				}, {
					url: "https://m.360buyimg.com/babel/jfs/t1/188863/30/9513/108197/60d15822E9d276cf7/d768989528c094e4.png",
					action: ""
				}];
				this.banners = data;
			},
			//获取图标列表
			geticonLists() {
				var data = [{
						url: "../../static/icon/redu.png",
						name: "热卖众筹"
					}, {
						url: "../../static/icon/ji.png",
						name: "家禽"
					},
					{
						url: "../../static/icon/rou.png",
						name: "鲜肉"
					},
					{
						url: "../../static/icon/shucai.png",
						name: "蔬菜"
					}, {
						url: "../../static/icon/shuiguo.png",
						name: "水果"
					}
				];
				this.iconLists = data;
			},
			//获取特价商品
			gettejia() {
				var data = [];
				for (var i = 0; i < 5; i++) {
					var p = {
						id: 1,
						url: "../../static/sucai/m10.png",
						price: 3899,
						tag: "特价"
					};
					p.tag+=i;
					p.id=i+1;
					p.price+=i;
					data.push(p);
				};
				this.tejiaLists=data;
				//console.log(data);
			},
			//获取商品列表
			getgoodsLists(){
				var data=[];
				for(var i=0;i<10;i++){
					var p={
						id:1,
						title:'震撼发布仅售3998元还不快抢',
						tag1:true,
						shop:"大米旗舰店",
						tag2:true,
						tag3:true,
						url:"../../static/sucai/m10.png",
						price:3899,
						num:1000
					};
					data.push(p);
				};
				this.goodsLists=data;
			}
		}
	}
</script>

<style>
	.swiperimg {
		width: 750upx;
		height: 250upx;
	}

	.zhongchou {
		display: flex;
		justify-content: space-between;
		height: 90upx;
		align-items: center;
		padding-left: 20upx;
		padding-right: 20upx;

	}

	.icon-item image {
		width: 100upx;
		height: 100upx;
		text-align: center;
	}

	.icon-father {
		border-top: 0.5upx solid #e7e7e7;
		display: flex;
		justify-content: space-around;
		padding-top: 30upx;
		padding-bottom: 30upx;
	}

	.tejia {
		margin-top: 20upx;
	}

	.tejiabar {
		padding-left: 20upx;
		padding-right: 20upx;
	}

	.image1 {
		width: 130upx;
		height: 130upx;
	}
	.zhanwei{
		height:var(--status-bar-height);
		width: 100%;
	}
</style>
