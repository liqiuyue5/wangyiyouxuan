<template>
	<view>
		<!-- 导航条 -->
		<!-- <scroll-view scroll-x="true"  class="scrollContainer"> -->
		<view class="inv-content">
				<view class="inv-h-w">
						<view :class="['inv-h',Inv==0?'inv-h-se':'']" @click="Inv=0">14:00<view class="qiang">已开抢</view></view>
						<view :class="['inv-h',Inv==1?'inv-h-se':'']" @click="Inv=1">18:00<view class="qiang">已开抢</view></view>
						<view :class="['inv-h',Inv==2?'inv-h-se':'']" @click="Inv=2">22:00<view class="qiang">已开抢</view></view>
						<view :class="['inv-h',Inv==3?'inv-h-se':'']" @click="Inv=3">10:00<view class="qiang">已开抢</view></view>
						<view :class="['inv-h',Inv==4?'inv-h-se':'']" @click="Inv=4">14:00<view class="qiang">已开抢</view></view>
				</view>
		</view>

		<!-- 内容区 -->
			<view class="" v-show="Inv == 0">
					我是选项卡一
			</view>
			<view class="" v-show="Inv == 1">
					我是选项卡二
			</view>
			<view class="two-nei" v-show="Inv == 2">
				<!-- 轮播图 -->
				<view class="uni-padding-wrap">
					<view class="page-section swiper">
						<view class="page-section-spacing">
							<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration" :circular="circular">
								<swiper-item>
									<view class="swiper-item uni-bg-red"><image class="img" src="../../static/e.webp" mode=""></image></view>
								</swiper-item>
								<swiper-item>
									<view class="swiper-item uni-bg-green"><image class="img" src="../../static/w.webp" mode=""></image></view>
								</swiper-item>
							</swiper>
						</view>
					</view>
				</view>
				<view class="showContainer" >
					<view class="time-last">
						<view class="one">
							本场还有
						</view>
						<uni-countdown color="#ffffff" background-color="#000000" :show-day="false" :hour="03" :minute="31" :second="50" class="time"></uni-countdown>
						<view class="one">
							结束
						</view>
					</view>
					<view class="show-one" v-for="(item,index) in itemlist" :key="index">
						<view class="img-shoping">
							<image class="shafa" :src="item.listPicUrl"></image>
						</view>
						<view class="biaoqi">
							<h3>{{item.itemName}}</h3>
							<span class="orang">{{item.itemTitle | ellipsis}}</span></br>
							<span class="money-icn">￥<span class="money">{{item.retailPrice}}</span></span>
							<view class="tiao">
								<view class="jindu">
									<view class="color-tiao">
										
									</view>
									<view class="yiqiang">
										已抢84件
									</view>
									<view>
										42%
									</view>
								</view>
								<view class="mashang">
									<span>马上抢</span>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="" v-show="Inv == 3">
					我是选项卡四
			</view>
			<view class="" v-show="Inv == 4">
					我是选项卡五
			</view>
	</view>
</template>

<script>
	import {uniCountdown} from '@dcloudio/uni-ui/lib/uni-countdown/uni-countdown'
	
	 export default {
			data() {
					return {
							Inv:2,
							background: ['color1', 'color2'],
							indicatorDots: true,
							autoplay: true,
							circular:true,
							interval: 5000,
							duration: 500,
							itemlist:[]
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
			filters: {
			    ellipsis (value) {
			      if (!value) return ''
			      if (value.length > 10) {
			        return value.slice(0,10) + '...'
			      }
			      return value
			    }
			  },
			onLoad() {
				uni.request({
				    url: 'http://localhost:3000/dazhe', 
				    
				    success: (res) => {
				        console.log(res.data.data.itemList);
				        this.itemlist = res.data.data.itemList
				    }
				})
			}
	}
</script>

<style>
	/* 导航条 */
	.inv-content{
		background-color:#ff3243;
		height:300upx;
	}
	.inv-h-w{
		background-image:url('../../static/q.webp');
		height: 150upx;
		display: flex;
		}
	.inv-h{
		font-weight: bold;
		flex: 1;
		font-size: 30upx;
		text-align: center;
		color: #C9C9C9;
		height: 100upx;
		line-height: 100upx;
		/* position: relative; */
		/* padding-top: 35upx; */
		}
	.qiang{
		font-size: 25upx;
		line-height: 3upx;
		/* position: absolute; */
		/* top:10upx; */
		}
	.inv-h-se{
		color: #FFFFFF;
		font-size: 45upx;
		}
	/* 轮播图 */
	.img{
		width: 100%;
		height: 100%;
		border-radius: 5%;
	}
	.swiper-item {
		width: 100%;
		height: 100%;
		}
	.swiper{
		height: 300upx;
	}
	.uni-padding-wrap{
		width: 700upx;
		position: relative;
		top: -150upx;
		margin: 0 auto;
	}
	/* 内容去 */
	.showContainer{
		width: 700upx;
		position: relative;
		top: -130upx;
		margin: 0 auto;
		border-radius: 20upx;
		margin-top: 30upx;
		background-color: #FFFFFF;
	}
	.show-one{
		border-top: #C0C0C0 solid 1upx;
		padding: 30upx 0;
		display: flex;
		width: 620upx;
		height: upx;
		margin: 0 auto;
		justify-content: space-between;
	}
	.img-shoping{
		width: 245upx;
		height: 245upx;
		/* float: left; */
	}
	image{
		width: 100%;
		height: 100%;
	}
	.biaoqi{
		margin-left: 35upx;
		width: 420upx;
		height: 245upx;
	}
	.orang{
		color: #F5992C;
		font-size: 25upx;
	}
	.biaoqi h3{
		font-weight: bold;
		font-size: 35upx;
	}
	.money-icn{
		color: #DD1A21;
		font-size: 25upx;
	}
	.money{
		font-size: 40upx;
		font-weight:bold;
	}
	.tiao{
		width: 370upx;
		height:60upx ;
/* 		margin-top: 30upx; */
		display: flex;
		margin-bottom: 0;
		justify-content: space-between;
	}
	.jindu{
		width: 190upx;
		height: 25upx;
		font-size: 18upx;
		color: #FFFFFF;
		background-color: #FFC8B2;
		margin-top: 20upx;
		border-radius:20upx;
		display: flex;
		justify-content: space-between;
	}
	.color-tiao{
		border-radius:20upx;
		width: 20upx;
		background-color: #FF1D25;
	}
	.yiqiang{
		width: 130upx;
	}
	/* 倒计时 */
	.time-last{
		margin: 20upx auto;
		display: flex;
		height: 100upx;
		/* line-height: 100upx; */
		justify-content: space-between;
		width: 450upx;
		/* border-bottom: 1upx #C0C0C0 solid; */
	}
	.one{
		font-size: 33upx;
		margin-top: 30upx;
	}
	.time{
		margin-top: 20upx;
	}
	.mashang{
		width: 110upx;
		height: 60upx;
		color: #FFFFFF;
		font-size: 30upx;
		padding-left: 20upx;
		font-weight: bold;
		line-height: 60upx;
		border-radius: 20upx;
		background-color: #FF4753;
	}
	page{
		background-color: #EEEEEE;
		}
		
</style>
