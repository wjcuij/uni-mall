<template>
	<view>
		<!-- 头部开始 -->
		<view class="caozuo">
			<view>
		    <checkbox-group class="flex align-center" @change="changeAll">
			<checkbox :checked="checked" :class="checked==true?'checked':''" class="round sx-check"></checkbox>
				<text style="font-size: 110%;margin-left: 10upx;">全选</text>
			</checkbox-group>
			</view>
			<view>
				<view @tap="deleteAll" class="cu-btn sm round"><text class="cuIcon-delete"></text>删除</view>
			</view>
		</view>
		<!-- 头部结束 -->
		<!-- 购物车内容开始 -->
		<view class="cart-content">
			<view class="cart-item bg-white">
				<view class="flex align-center">
					<checkbox-group class="flex align-center" @change="changeAll2">
					<checkbox :checked="checked1" :class="checked1==true?'checked':''" class="round sx-check"></checkbox>
					
						<text style="font-size: 110%;margin-left: 10upx;">全选</text>
					</checkbox-group>
					<image src="../../../static/sucai/8.png"></image>
				</view>
				<view class="cart-ycontent" style="width: 450upx;">
					<view class="cart-title">手机名字</view>
					<view>
						<view class="text-gray">类型:x</view>
						<view class="flex justify-between">
							<view class="text-red text-bold text-lg">￥200.0</view>
						    <uni-number-box @change="changejishu" style="margin-right: 40upx;" :min="0" :max="999"></uni-number-box>
						</view>
					</view>
					
				</view>
			</view>
		</view>
		<!-- 购物车内容结束 -->
		<!-- 结算区域开始 -->
		<view class="heji flex justify-between align-center">
			<view style="font-size: 110%;">合计<text class="text-orange">￥{{sum}}</text></view>
			<view>
				<view class="cu-btn bg-gradual-red round">去结算</view>
			</view>
		</view>
		<!-- 结算区域结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				checked:true,
				checked1:true,
				sum:0
			}
		},
		methods: {
			changeAll(e){
				// console.log(this.checked)
				this.checked ? this.checked = false : this.checked = true;
			},
			changeAll2(){
				console.log(this.checked1)
				this.checked1 ? this.checked1 = false : this.checked1 = true;
			}
		}
	}
</script>

<style>
body{
	background: #8799A3;
}
.sx-check{
	transform: scale(0.7);
}
.cart-ycontent{
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	padding-top: 8upx;
	padding-bottom: 8upx;
}
.cart-title{
	font-size: 110%;
	font-weight: bold;
	width: 450upx;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;

}
.caozuo{
	position: fixed;
	top:0upx;
	/*#ifdef H5*/
	top:90upx;
	/*#endif*/
	background-color: white;
	display: flex;
	justify-content: space-between;
	height: 80upx;
	align-items: center;
	width: 750upx;
	padding-left: 30upx;
	padding-right: 30upx;
}
.cart-content{
	margin-top:82upx;
	margin-bottom: 200upx;
	
}
.cart-item{
	display: flex;
	justify-content: space-between;
	padding: 20upx 20upx 20upx 20upx;
	margin-top: 20upx;
}
.cart-item image{
	width: 200upx;
	height: 200upx;
}
.heji{
	position: fixed;
	bottom: 0upx;
	/*#ifdef H5*/
	bottom: 100upx;
    /*#endif*/
	width: 750upx;
	height: 100upx;
	background-color: white;
	padding-left: 30upx;
	padding-right: 30upx;
}
</style>
