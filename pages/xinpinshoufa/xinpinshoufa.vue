<template>
	<div class="wrapper">
		<!-- 头部开始 -->
		<div class="header"  >
			<a href="#" @click="hhh()">
				<i class='iconfont icon-home'></i>
			</a>
			<a href="">
				<span>网易严选</span>
			</a>
			<a href="#">
				<i class='iconfont icon-tubiaolunkuo-'></i>
			</a>
			<a href="#">
				<i class='iconfont icon-gouwuche'></i>
			</a>
		</div>
		<!-- 头部结束 -->
		<!-- 内容区 -->
		<div class="container">
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item, index) in lunboDatas.newItemAds" :key='index'>
					<image :src="item.picUrl" mode=""></image>
				</swiper-item>
			</swiper>
			<!-- 轮播结束 -->
			<!-- 推荐关注开始 -->
			<div class="tuijianguanzhu">
				<h3>推荐关注</h3>
				<div class="hop">
					<div class="hopcontent" v-for="(item, index) in enterxinpinone" :key='index'>
						<div class="hopleft">
							<image :src="item.primaryPicUrl" mode=""></image>
						</div>
						<div class="hopright">
							<p>"</p>
							<!-- <p class="ptitle">食养珍品，高端礼赠</p> -->
							<p class="ptitle">{{item.promTag}}</p>
							
							<span class="xinpinchangxian">新品尝鲜</span>
							<!-- <h4>50%即食燕窝礼盒 70毫升*8瓶</h4> -->
							<h4>{{item.name}}</h4>
							<span class="price">¥{{item.retailPrice}}</span>
						</div>
					</div>
					
				</div>
				<div class="tjgzlist">
					<ul>
						<li v-for="(item, index) in enterxinpin" :key='index'>
							<a href="#">
								<div class="tjgzshoplist">
									<div class="tupiantop">
										<!-- <image src="https://yanxuan-item.nosdn.127.net/66265705e60b9cef759575d969e20bf8.png" mode=""></image> -->
										<image :src="item.primaryPicUrl" mode=""></image>
										
									</div>
									<div class="tupianbottom">
										<div class="tbleft">
											<p>{{item.promTag}}</p>
											<p>¥{{item.retailPrice}}</p>
										</div>
										<div class="tbright">
											<span>{{item.listPromBanner.content}}</span>
										</div>
									</div>
								</div>
								<p class="content">{{item.name}}</p>
								<div class="shopprice">
									<span class="leftprice">¥{{item.retailPrice}}</span>
									<span class="rightprice">¥{{item.counterPrice}}</span>
								</div>
								<div class="fansprice">
									<span class="fptext">新品粉丝价</span>
								</div>
							</a>
						</li>
					</ul>
				</div>
			</div>
			<!-- 推荐关注结束 -->
			<!-- 全部新品 -->
			<div class="quanbuxinpin" >
				<h3>全部新品</h3>
				<div class="qbsptitle" :class="{guding:scroll>1216}">
					<ul>
						<li>综合</li>
						<li>价格</li>
						<li>分类</li>
						<li>制造商</li>
					</ul>
				</div>
				<div class="benqixinpin">
					<div class="bqxptitle">
						<div class="xiaoshuxian"></div>
						<h4>本期新品</h4>
					</div>
					<ul>
						<li v-for="(item1, index) in quanbuxinpinDatas.newItems.itemList" :key='index'>
							<a href="#">
								<div class="tjgzshoplist">
									<div class="tupiantop">
										<!-- <image src="https://yanxuan-item.nosdn.127.net/66265705e60b9cef759575d969e20bf8.png" mode=""></image> -->
										<image :src="item1.listPicUrl" mode=""></image>
										
									</div>
									<div class="tupianbottom">
										<div class="tbleft">
											<p>{{item1.promotionDesc}}</p>
											<p>¥{{item1.retailPrice}}</p>
										</div>
										<div class="tbright">
											<span>{{item1.listPromBanner.content}}</span>
										</div>
									</div>
								</div>
								<!-- <p class="content">澳大利亚制造 深海鱼油胶囊365粒装</p> -->
								<p class="content">{{item1.name}}</p>
								<div class="shopprice">
									<span class="leftprice">¥{{item1.retailPrice}}</span>
									<span class="rightprice">¥{{item1.counterPrice}}</span>
								</div>
								<div class="fansprice">
									<span class="fptext">新品粉丝价</span>
								</div>
							</a>
						</li>
					</ul>
				</div>
				
			</div>
			<!-- 全部新品结束 -->
			<!-- 众筹上新开始 -->
			<div class="zhongchoushangxin">
				<div class="zcsxtitle">
					<a href="#">
						<span>众筹上新推荐</span>
						<i class="iconfont icon-jiantou"></i>
					</a>
				</div>
				<div class="zhongchou" v-for="(item2, index) in zhongchoushangxinDatas.zcItems" :key='index'>
					<div class="zhongchouleft">
						<image :src="item2.picUrl" mode=""></image>
					</div>
					<div class="zhongchouright">
						<div class="zhongchoutitle">{{item2.name}}</div>
						<div class="zhongchouprice">
							<span class="small">¥</span>
							<span class="zcp">{{item2.minPrice}}.00</span>
							<span class="small">起</span>
						</div>
						<div class="jindu">
							<div class="jindutiao"></div>
							<span>{{item2.actualAmountPercent}}%</span>
						</div>
						<div class="zhichirenshu">
							<div class="left">
								<i class="iconfont icon-yonghu"></i>
								<span>{{item2.actualNum}}人已支持</span>
							</div>
							<div class="right">
								支持项目
							</div>
						</div>
					</div>
				</div>
			</div>
			<!-- 众筹上新结束 -->
			<!-- 新品放映室开始 -->
			<div class="xinpinfangying">
				<div class="title">
					<a href="#">新品放映室</a>
				</div>
				<scroll-view scroll-x="true" class="scrollfangying">
					<view class="fongyinglist" v-for="(item3, index) in xinpinfangyingDatas.screeningRoom.screeningList" :key='index'>
						<div class="top">
							<!-- <image src="https://yanxuan.nosdn.127.net/e1d3aa8d8420f4797c8d200f8f5ed2d9.jpg" mode=""></image> -->
							<image :src="item3.scenePicUrl" mode=""></image>
						</div>
						<div class="bottom">
							<p class="btop">{{item3.title}}</p>
							<p class="bbottom">{{item3.subtitle}}</p>
						</div>
					</view>
				</scroll-view>
			</div>
			<!-- 新品放映室结束 -->
			<div class="xinpinyugao">
				<h4>新品预告</h4>
				<ul>
					<li v-for="(Item, index) in xinpinyugaoDatas.data" :key='index'>
						<a href="#">
							<div class="headertupian">
								<div class="toptupian">
									<!-- <image src="https://yanxuan-item.nosdn.127.net/0841f96ee9a6f05bceb358b15cb8da25.png" mode=""></image> -->
									<image :src="Item.listPicUrl" mode=""></image>
								</div>
								<div class="bottombiaoti">
									{{Item.simpleDesc}}
								</div>
							</div>
							<div class="shoptitle">
								<span>{{Item.name}}</span>
							</div>
							<div class="shopprice">
								<span>￥{{Item.couponPrice}}</span>
							</div>
							<div class="jijiangshangjia">
								<span>即将上架</span>
							</div>
						</a>
					</li>
				</ul>
			</div>
		</div>
		<!-- 内容区结束 -->
		
		<!-- 这个div是防止style合住,没卵用 -->
		<!-- <div class="meiyong"></div> -->
	</div>
</template>

<script>
	import request from '../../utils/request.js'
	export default {
		data() {
			return {
				scroll:0,
				xinpinyugaoDatas:{},
				lunboDatas:{},
				xinpinchangxianDatas:{},
				quanbuxinpinDatas:{},
				zhongchoushangxinDatas:{},
				xinpinfangyingDatas:{}
			}
		},
		
		
		async mounted(){
			
			uni.pageScrollTo({
				    // scrollTop: 5074,  //距离页面顶部的距离
				    // duration: 300
				});
			this.xinpinyugaoDatas = await request('/getPreNewItem')
			this.lunboDatas = await request('/lunbo')
			this.xinpinchangxianDatas = await request('/xinpinchangxian')
			this.quanbuxinpinDatas = await request('/quanbuxinpin')
			this.zhongchoushangxinDatas = await request('/zhongchoushangxin')
			this.xinpinfangyingDatas = await request('/xinpinfangying')
			// console.log(this.xinpinyugaoDatas)
		},
		computed:{
			enterxinpin(){
				if (this.xinpinchangxianDatas.editorRecommendItems) {
					return this.xinpinchangxianDatas.editorRecommendItems.slice(-6)
				}
			},
			enterxinpinone(){
				if (this.xinpinchangxianDatas.editorRecommendItems) {
					return this.xinpinchangxianDatas.editorRecommendItems.slice(0,1)
				}
			}
		},
		// onLoad() {
		// 	// var num = 0
		// 	uni.pageScrollTo({
		// 	    scrollTop: 5400,  //距离页面顶部的距离
		// 	    duration: 300
		// 	});
		// 	this.setData({
		// 		scroll:num
		// 	})
		// },
		onPageScroll(res){
			
			// console.log(res.scrollTop);//距离页面顶部距离
			// this.num = res.scrollTop
			if(res.scrollTop>=1217){
				this.setData({
					scroll:res.scrollTop
				})
			}
			
			
		},
		
		onShow() {
			
		},
		methods: {
			hhh(){
				uni.switchTab({
				    url: '/pages/index/index'
				});
			},
		}
	}
</script>

<style lang="stylus">
	.wrapper
		width 100%
		height 100%
		background rgb(238,238,238)
		.header
			width 710upx
			height 87upx
			padding 0 16upx 0 24upx
			background white
			// border 1upx solid red
			display flex
			vertical-align middle
			line-height 87upx
			position fixed
			top 0
			z-index 99
			background white
			margin-bottom 100upx
			a
				.iconfont
					font-size 50upx
				.icon-tubiaolunkuo-
					margin 0 30upx
				span 
					margin 0 100upx 0 230upx
		.container
			background rgb(238,238,238)
			swiper
				width 100%
				height 369.984upx
				margin-top 87upx
				margin-bottom: 21upx;
				background-color white
				swiper-item
					image
						width 100%
						height 369.984upx
			.tuijianguanzhu
				background white
				margin-bottom: 20upx
				h3
					width 100%
					height 110upx
					text-align center
					line-height 110upx
				.hop
					width 710upx
					height 279.984upx
					padding 0 20upx
					margin-bottom 30upx
					.hopcontent
						border 1px solid #d9d9d9
						width 708upx
						height 277.984upx
						display flex
						.hopleft
							width 279.984upx
							height 279.984upx
							margin-right 17upx
							image
								width 279.984upx
								height 279.984upx
						.hopright
							width 411.016upx
							height 277.984upx
							.ptitle
								color: #7f7f7f;
								font-size 26upx
								margin-bottom: 17upx;
							.xinpinchangxian
								background-color: #dea34c;
								color white
								font-size 20upx
								padding 0 16upx
								margin-bottom:1upx;
							.price
								color red
				.tjgzlist
					width 100%
					height 1841.44upx
					ul
						display flex
						justify-content: space-between
						flex-wrap wrap
						padding 0 20upx
						li
							width 345upx
							a
								.tjgzshoplist
									width 345upx
									height 389.844upx
									.tupiantop
										width 345upx
										height 345upx
										image
											width 345upx
											height 345upx
									.tupianbottom
										width 345upx
										height 56upx
										display flex
										vertical-align bottom
										position relative
										.tbleft
											width 121.969upx
											height 56upx
											font-size 16upx
											color white
											background rgb(192,7,14)
											text-align center
											line-height 28upx
											margin-top -8upx
											border-top-right-radius 20upx
										.tbright
											width 217.031upx
											height 48upx
											padding-left 6upx
											background rgb(221,26,33)
											color white
											line-height 48upx
											font-size 28upx
								.content
									display block
									width 345upx
									height 78upx
									margin-top 16upx
								.shopprice
									width 345upx
									height 48upx
									line-height 48upx
									.leftprice
										color red
										font-size 37.667upx
									.rightprice
										text-decoration line-through
										color #999
										font-size 27upx
										margin-left 10upx
								.fansprice
									width 345upx
									height 33upx
									margin 4upx 0 12upx 0
									font-size 16upx
									color #DD1A21;
									// border 1upx solid red
									.fptext
										width 90upx
										height 28upx
										padding 0 8upx
										border 0.5upx solid #DD1A21
										border-radius 10upx
										
			.quanbuxinpin
				width 750upx
				height 6633upx
				background white
				margin-bottom: 20upx
				h3
					width 100%
					height 110upx
					text-align center
					line-height 110upx
				.guding
					position fixed
					top 200upx
					right 0 
				.qbsptitle
					width 750upx
					height 81upx
					// position fixed
					// top 200upx
					// right 0 
					ul
						width 750upx
						height 80upx
						border-bottom 1upx solid #d9d9d9
						background-color: #fafafa;
						display flex
						li
							
							width 174.75upx
							height 80upx
							text-align center
							line-height 80upx
				.benqixinpin
					width 750upx
					height 7416.750upx
					.bqxptitle
						width 720upx
						height 90upx
						// padding-left 30upx
						padding 30upx
						box-sizing border-box
						// display flex
						// vertical-align middle
						// line-height 90upx
						.xiaoshuxian
							display block
							width 10upx
							height 34upx
							background rgb(221,26,33)
							float left
							// vertical-align middle
							// line-height 45upx
						h4
							margin-left 20upx
							vertical-align middle
							// float left
					ul
						width 750upx
						// height 7248.75upx
						display flex
						justify-content space-between
						flex-wrap wrap
						padding 0 20upx
						box-sizing border-box
						li
							width 345upx
							height 574.81upx
							a
								.tjgzshoplist
									width 345upx
									height 389.844upx
									background rgb(244,244,244)
									.tupiantop
										width 345upx
										height 345upx
										image
											width 345upx
											height 345upx
									.tupianbottom
										width 345upx
										height 56upx
										display flex
										vertical-align bottom
										position relative
										.tbleft
											width 121.969upx
											height 56upx
											font-size 16upx
											color white
											background rgb(192,7,14)
											text-align center
											line-height 28upx
											margin-top -8upx
											border-top-right-radius 20upx
										.tbright
											width 217.031upx
											height 48upx
											padding-left 6upx
											background rgb(221,26,33)
											color white
											line-height 48upx
											font-size 28upx
								.content
									display block
									width 345upx
									height 78upx
									margin-top 16upx
								.shopprice
									width 345upx
									height 48upx
									line-height 48upx
									.leftprice
										color red
										font-size 37.667upx
									.rightprice
										text-decoration line-through
										color #999
										font-size 27upx
										margin-left 10upx
								.fansprice
									width 345upx
									height 33upx
									margin 4upx 0 12upx 0
									font-size 16upx
									color #DD1A21;
									// border 1upx solid red
									.fptext
										width 90upx
										height 28upx
										padding 0 8upx
										border 0.5upx solid #DD1A21
										border-radius 10upx
			.zhongchoushangxin
				width 750upx
				height 996upx
				background white
				margin-bottom: 20upx
				.zhongchou
					width 680upx
					height 249.938upx
					padding 25upx 40upx 25upx 30upx
					display flex
					.zhongchouleft
						width 240upx
						height 210upx
						image
							width 210upx
							height 210upx
					.zhongchouright
						width 440upx
						height 249.969upx
						.zhongchoutitle
							width 440upx
							height 78upx
							margin-top 6upx
						.zhongchouprice
							width 440upx
							height 35upx
							margin-top 12upx
							color #F48F18
							.small
								font-size 27upx
							.zcp
								font-size 37upx
						.jindu
							width 440upx
							height 39upx
							margin-top 16upx
							display flex
							color: #F48F18;
							display flex
							align-items: center;
							.jindutiao
								width 330upx
								height 20upx
								border-radius 5upx
								background: #F48F18;
						.zhichirenshu
							width 440upx
							height 48upx
							margin-top 16upx
							display flex
							justify-content space-between
							.left
								display flex
								span
									font-size 26upx
							.right
								width 138upx
								height 46upx
								border 1upx solid #F48F18
								color #F48F18
								text-align center
								font-size 26upx
				.zcsxtitle
					width 100%
					height 110upx
					a
						display flex
						align-items: center
						justify-content: center
						line-height 110upx
						i
							vertical-align bottom
			.xinpinfangying
				width 744upx
				height 680upx
				padding-left 6upx
				margin 20upx 0
				background white
				margin-bottom: 20upx
				.title
					width 744upx
					height 110upx
					text-align center
					line-height 110upx
				.scrollfangying
					width 744upx
					height 542upx
					// border 1upx solid red
					white-space nowrap
					// display flex
					.fongyinglist
						width 357.984upx
						height 541.969upx
						margin-left 24upx
						display inline-block
						// display flex
						.top
							width 357.984upx
							height 357.984upx
							image
								width 357.984upx
								height 357.984upx
						.bottom
							width 325.984upx
							height 143.984upx
							padding 20upx 16upx
							background-color: #C9453F
							color white
							// white-space wrap
							.btop
								overflow hidden
								white-space nowrap
								text-overflow ellipsis
							.bbottom
								display -webkit-box
								-webkit-box-orient vertical
								-webkit-line-clamp 2
								overflow hidden
								white-space wrap
			.xinpinyugao
				width 100%
				height 1337.630upx
				background white
				h4
					width 100%
					height 110upx
					text-align center
					line-height 110upx
				ul
					width 750upx
					height 1227.630upx
					display flex
					justify-content space-between
					flex-wrap wrap
					padding 0 20upx
					box-sizing border-box
					li
						width 345upx
						height 580.813upx
						a
							.headertupian
								width 345upx
								height 389.844upx
								.toptupian
									width 345upx
									height 345upx
									image
										width 345upx
										height 345upx
								.bottombiaoti
									width 325upx
									height 36upx
									padding 6upx 10upx
									// background-color rgb(241,236,226)
									background #F1ECE2
									color #9F8A60
									overflow hidden
									white-space nowrap
									text-overflow ellipsis
									font-size 26upx
							.shoptitle
								width 345upx
								height 78upx
								margin-top 16upx
								span
									font-size 27upx
							.shopprice
								width 345upx
								height 48upx
								span
									font-size: 37upx;
									line-height: 48upx;
									color: #DD1A21;
							.jijiangshangjia
								width 345upx
								height 33upx
								margin 4upx 0 12upx
								span
									width 72upx
									height 28upx
									padding 0 8upx
									font-size 19upx
									color #DD1A21
									border: 1px solid #DD1A21;
									border-radius 10upx
		// .meiyong
		// 	width 100%
		// 	height 50upx
		// 	background #bfa
</style>
