<template>
	<view>
		<view class="list_box">
			<view class="item_box border-b" v-for="(item,index) in 2" :key="index">
				<view class="item_top">
					<view class="item_name">{{item}}</view>
					<view class="item_phone">{{item.tel}}</view>
					<!-- <view class="item_home">家</view> -->
				</view>
				<view class="item_bottom">
					<view class="item_map">
						{{item.addr}}
					</view>
					<view class="item_icon"></view>
				</view>
			</view>
		</view>
		<navigator class="btn_box" url="NewAddress" hover-class="none"><text>+</text>新增收货地址</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				siteList:[]
			};
		},
		mounted() {
			this.getMyShippingAddr();
		},
		methods:{
			getMyShippingAddr(){
				// 我的收货地址
				this.$H.post('/member/userShippingAddr/getMyShippingAddr', {}, {
					token: true,
					
				}).then(res => {
					console.log('我的收货地址', res);
					if (res.code == 1) {
						this.siteList=res.data;
					}
				})
			},
			
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #FFFFFF;
	}
.list_box{
	padding: 0 24rpx;
	.item_box{
		padding: 20rpx 0;
		.item_top{
			display: flex;
			align-items: center;
			margin-bottom: 20rpx;
			.item_name{
				font-size: 35rpx;
				font-weight: bold;
			}
			.item_phone{
				font-size: 30rpx;
				font-weight: bold;
				margin-left: 80rpx;
			}
			.item_home{
				font-size: 24rpx;
				background-color:#4D88FF;
				padding: 0 15rpx;
				border-radius: 6rpx;
				color: #FFFFFF;
				margin-left: 10rpx;
			}
		}
	    .item_bottom{
			display: flex;
			align-items: center;
			justify-content: space-between;
			font-size: 24rpx;
			color: #666666;
			.item_icon{
			width: 40rpx;
			height: 40rpx;
			border: 1rpx solid #CCCCCC;
			}
		}
	}
}
.btn_box{
	position: fixed;
	bottom: 100rpx;
	background-color: red;
	width: 90%;
	margin-left: 5%;
	height: 88rpx;
	line-height: 88rpx;
	border-radius: 60rpx;
	text-align: center;
	color: #FFFFFF;
	font-size: 32rpx;
	>text{
		margin-right: 20rpx;
		font-weight: bold;
		font-size: 36rpx;
	}
}
</style>
