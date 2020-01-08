<template>
	<div>
		<view>
			<image src="../../static/a.jpg"  class="img-T"></image>
		</view>
		<view class="inv-content">
				<view class="inv-h-w">
						<view :class="['inv-h',Inv==0?'inv-h-se':'']" @click="Inv=0">编辑推荐</view>
						<view :class="['inv-h',Inv==1?'inv-h-se':'']" @click="Inv=1">24小时热销榜</view>
						<view :class="['inv-h',Inv==2?'inv-h-se':'']" @click="Inv=2">人气周榜</view>
						<view :class="['inv-h',Inv==3?'inv-h-se':'']" @click="Inv=3">热销周榜</view>
				</view>
		</view>
		<view class="" v-show="Inv == 0">
				<div class='tab-container'>
					<div class="commodity-list">
						<div class="commodity-item" v-for="(item,index) in renqituijian" :key="index">
							<image :src="item.listPicUrl"></image>
							<span class="title">{{item.name}}</span>
							<span class='money'>{{item.retailPrice}}</span>
							<span class='sign'>年货特惠</span>
						</div>
					</div>
				</div>
		</view>
		<view class="" v-show="Inv == 1">
				我是选项卡二
		</view>
		<view class="" v-show="Inv == 2">
				我是选项卡二
		</view>
		<view class="" v-show="Inv == 3">
				我是选项卡二
		</view>
	
		
	</div>
	</template>

<script>
import {uniCountdown} from '@dcloudio/uni-ui/lib/uni-countdown/uni-countdown'
	
	 export default {
			data() {
					return {
							Inv:0,
							renqituijian:[]
					}
			},
			components: {uniCountdown},
			methods: {
					changeTab(Inv){
							that.navIdx = Inv;
							 
					},
					changeIndicatorDots(e) {
						this.indicatorDots = !this.indicatorDots
					},
					changeAutoplay(e) {
						this.autoplay = !this.autoplay
					},
					intervalChange(e) {
						this.interval = e.target.value
					},
					durationChange(e) {
						this.duration = e.target.value
					}
			},
			onLoad() {
				uni.request({
				    url: 'http://localhost:3000/renqituijian', 
				    
				    success: (res) => {
				        console.log(res.data.renqituijian);
				        this.renqituijian = res.data.renqituijian
				    }
				})
			}
	}
</script>
<style>
	.img-T{
		/* background-color: #007AFF; */
		height: 300upx;
	}
	/* 导航条 */
	.inv-content{
		background-color:#FFFFFF;
	}
	.inv-h-w{
		height: 100upx;
		display: flex;
		}
	.inv-h{
		/* font-weight: bold; */
		/* width: 50upx; */
		flex: 1;
		font-size: 30upx;
		text-align: center;
		color: #000000;
		height: 100upx;
		line-height: 100upx;
		/* position: relative; */
		/* padding-top: 35upx; */
		}
	.inv-h-se{
		color: #FF1D25;
		border-bottom: #FF1D25 solid 2upx;
		}
</style>
<style lang="stylus" scoped>
	.tab-container
		padding 20upx
		.commodity-list
			.commodity-item:nth-child(odd)
				margin-right 16upx
			.commodity-item
				width 350upx
				display flex
				flex-direction column
				float left
				margin-bottom 30upx
				image
					width 100%
					height 350upx
					margin-bottom 30upx
				.title
					font-size 35upx
					height 37
					line-height 1.2
				.money
					color #E44B51
					font-size 35upx
				.sign
					border-radius 30upx
					border 1upx solid #E96C70
					font-size 20upx
					color #E96C70
					padding  3upx 5upx 5upx 5upx
					width 80upx
					line-height 100%
</style>
