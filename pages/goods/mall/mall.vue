<template>
	<view>
		<!--搜索框-->
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
		<!--内容开始-->
		<view class="flex">
	
			<scroll-view class="bg-gray" scroll-y style="height:calc(100vh - 300upx);width:200upx;"><!--100vh-(导航栏最小高度100upx)-底部导航栏-->
		<!-- 	<view class="type-item bg-white text-bold cur" style="font-size: 120%;">
				<view class="shuxian bg-red"></view>选中的项
				</view> -->
				<view @tap="select(index)" :class="selected == index ? 'bg-white text-bold' : ''" :style="{fontSize:selected == index ? '120%' : '100%'}" v-for="(item,index) in types" :key="index" class="type-item">
					<view v-if="selected == index" class="shuxian bg-red"></view>
					{{item}}
				</view>
				
			</scroll-view>
			<scroll-view scroll-with-animation :scroll-into-view="'good-'+selected" class="bg-white" scroll-y style="height: calc(100vh - 310upx);width: 550upx;">
				<view :id="'good-'+i" style="border-bottom: 0.5upx #E7E7E7 solid;padding-bottom: 40upx;" v-for="(p,i) in goods" :key="i">
					<view class="text-black text-bold g-title" >{{types[i]}}</view>
					<view class="flex flex-wrap">
						<view v-for="(tp,ti) in p" :key="ti" style="width:275upx;" class="text-center flex-direction justify-center align-center">
							<image :src="tp.url" style="width:180upx;height:180upx;dispplay:block;"></image>
							<view class="flex justify-center align-center flex-direction">
								<view style="text-align: center;width: 180upx;white-space: nowrap;overflow: hidden;text-overflow: ellipsis;">{{tp.name}}</view>
								<view style="font-size: 120%;color: red;font-weight: bold;text-align: center;margin-right: 4upx;">￥{{tp.price}}</view>	
							</view>
						</view>
					</view>
					<view  class="text-bold text-black g-title">{{p.type_name}}</view>
					<!-- <view class="flex flex-wrap" :class="p.data.length==0?'justify-center':''">
						<view @tap="gotodetail(tp.goods_id)" class="flex justify-center align-center" style="width: 275upx;margin-top: 10upx;" v-for="(tp,ti) in p.data" :key="ti">
							<view>
								<image style="width: 180upx;height: 180upx;" :src="tp.image"></image>
								<view class="flex justify-center align-center flex-direction">
									<view style="text-align: center;width: 180upx;white-space: nowrap;overflow: hidden;text-overflow: ellipsis;">{{tp.name}}</view>
									<view style="font-size: 120%;color: red;font-weight: bold;text-align: center;margin-right: 4upx;">￥{{tp.price}}</view>	
								</view>
							</view>
						</view>
					    <view class="flex justify-center flex-direction align-center" v-if="p.data.length==0">
							<image style="width: 150upx;height: 150upx;filter: grayscale(100%);" src="/static/sucai/2.jpg"></image>
						     <view>暂无商品</view>
						</view>
					</view> -->
				</view>
			</scroll-view>
		</view>
		<!-- 内容结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				search:'',
				types:[],
				selected:0,
				goods:[]
			}
		},
		methods: {
			gettypes:function(){
				let data = [];
				for(let i = 0;i	< 100;i++){
					data.push('类目'+i)
				}
	
				this.types = data;
			},
			select:function(i){
				// console.log(this)
				this.selected = i;
			},
			getGoods:function(){
				let data = [];
				for(let i = 0;i<100;i++){
					let p = [];
					p.push({url:"/static/public-img/niup.jpg",name:this.types[i],price:parseInt(Math.random()*100)})
					p.push({url:"/static/public-img/niup.jpg",name:this.types[i],price:parseInt(Math.random()*100)}) 
					p.push({url:"/static/public-img/niup.jpg",name:this.types[i],price:parseInt(Math.random()*100)})
					data.push(p)
					}
					console.log(data)
					this.goods = data;
				}
			
			
		},
		onLoad(){
			this.gettypes();
			this.getGoods();
			console.log(1233)
		}
	}
</script>

<style>
	
.type-item{
	height:80upx;
	text-align:center;
	line-height:80upx;
	position: relative;
}
	
.shuxian{
	top:20rpx;
	position: absolute;
	width: 12rpx;
	height: 44rpx;
	left: 10rpx;
	
}
	.g-title{
		font-size: 110%;
		margin-top: 40upx;
		margin-bottom: 40upx;
		margin-left: 50upx;
	}
</style>
