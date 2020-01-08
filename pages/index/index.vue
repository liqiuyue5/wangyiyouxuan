<template>
	<div class="index">
		<div class="header">
			<image src="../../static/logo.png" mode=""></image>
			<div class="search">
				<i class='iconfont icon-sousuo'></i>
				<span class="input">搜索商品</span>
			</div>
			<button type="primary">登陆</button>
		</div>
		<scroll-view scroll-x="true"  class="scrollContainer">
			<view @click="changeNavIndex(index)" class="scrollItem" :class="{active: navIndex === (index)}" v-for="(navItem, index) in navList" :key='index'>
				{{navItem}}
			</view>
			<div class="down" @click="start" >
				<span :class="[rotate?'go':'aa']">
					<i class="iconfont icon-jiantou"></i>
				</span>
			</div>
			<div class="mask" v-show="isshow">
				<div class="all">
					<p>全部频道</p>
					<span v-for="(navItem, index) in navList" :key='index'>{{navItem}}</span>
				</div>
			</div>
		</scroll-view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" circular indicator-active-color="#fff">
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/96dd95c1c17f9522046746a877161550.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/970a7259190bb78d8184bf690a00e232.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/b9ddccbb7880a51bb357d086c8cf203d.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/a727bd85a581f50a7f6a9f8c23536437.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/0ccbc2f831adf2e025427ffc36118e01.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/529b3fb7437c1bd8e557439e902084a9.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/5e3b22826352644aff567c6be54076fb.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/2a1ebb5e41dd79922804e49c8fa70bdf.jpg?type=webp&imageView&quality=75&thumbnail=750x0" mode=""></image>
			</swiper-item>
			
		</swiper>
		<div class="m-index">
			<ul>
				<li>
					<image src="https://yanxuan.nosdn.127.net/a03dd909803b9ac032eba58b7253a2f6.png" mode=""></image>
					<p>网易自营品牌</p>
				</li>
				<li>
					<image src="https://yanxuan.nosdn.127.net/2d0402ffcd52b3ec3b07422681c42a89.png" mode=""></image>
					<p>30天无忧退货</p>
				</li>
				<li>
					<image src="https://yanxuan.nosdn.127.net/eb61ee48e8942dbd1784c9ee75ebe955.png" mode=""></image>
					<p>48小时快速退款</p>
				</li>
			</ul>
		</div>
		<div class="icon-all" >
			<div class="icon" v-for="(icon,index) in iconList" :key="index">
				<image  :src="icon.img"></image>
				<p>{{icon.p}}</p>
			</div>
		</div>
		<div class="advertisement">
			<div class="goods">
				<image src="https://yanxuan.nosdn.127.net/cceb27d92a3235feebf519fae3961a12.gif?imageView&quality=75" class="out"></image>
				<image src="https://yanxuan-item.nosdn.127.net/6ee5891c97a6cd11344fa31c71565bf7.png?imageView&thumbnail=168x0&quality=75" class="in"></image>
				<div class="prise">￥699</div>
			</div>
			<div class="proItem">
				<image src="https://yanxuan.nosdn.127.net/37265e43baa977efeb3fe8fa9d6363d4.png?quality=75&type=webp&imageView&thumbnail=750x0" mode=""></image>
			</div>
			<div class="floor clearfix">
				<a href="javascript:;">
					<image class="img1" src="https://yanxuan.nosdn.127.net/2fcc6d85b84e3253a87e012d434f03e1.png?quality=75&type=webp&imageView&thumbnail=375x0" mode=""></image>
					<image class="img2 img2_1" src="https://yanxuan-item.nosdn.127.net/ab5d901ca96b82797a5ca9d6809e88ee.png?quality=75&type=webp&imageView&thumbnail=160x160" mode=""></image>
				</a>
				<a href="javascript:;">
					<image class="img1" src="https://yanxuan.nosdn.127.net/370ee81f414fd800f4230fb45a1ea7c6.png?quality=75&type=webp&imageView&thumbnail=375x0" mode=""></image>
					<image class="img2 img2_2" src="https://yanxuan-item.nosdn.127.net/214fea8a9bbd3e4e4ec0f1572e1b6efb.png?quality=75&type=webp&imageView&thumbnail=160x160" mode=""></image>
				</a>
			</div>
			<div class="vip"><image src="https://yanxuan.nosdn.127.net/71c4f618480d2b43e01ac7b8adf12af0.png?quality=75&type=webp&imageView&thumbnail=750x0" mode=""></image></div>
			<div class="new_year">
				<image src="https://yanxuan.nosdn.127.net/839eb23bd1e8e511261c8e095282eff0.png?quality=75&type=webp&imageView&thumbnail=750x0" mode=""></image>
			</div>
			<div class="four">
				<div class="fir bac">
					<title>新年新衣</title>
					<p>全场不止五折</p>
					<image class="promGoods" src="https://yanxuan-item.nosdn.127.net/efa04c95e71505913246f8b800121362.png?quality=75&type=webp&imageView&thumbnail=160x160"></image>
				</div>
				<div class="sec bac">
					<title>美妆洗护</title>
					<p>开年限时5.5元</p>
					<image class="promGoods" src="https://yanxuan-item.nosdn.127.net/c35240dc88a30c7fb569bbca843f5e1a.png?quality=75&type=webp&imageView&thumbnail=160x160" mode=""></image>
				</div>
				<div class="tir bac">
					<title>餐厨特惠</title>
					<p>55元更新厨房</p>
					<image class="promGoods" src="https://yanxuan-item.nosdn.127.net/42fe3325353dd2856b871ff82a4b7c1c.png?quality=75&type=webp&imageView&thumbnail=160x160" mode=""></image>
				</div>
				<div class="fou bac">
					<title>全球洋货</title>
					<p>甄选年货45元</p>
					<image class="promGoods" src="https://yanxuan-item.nosdn.127.net/c0a002d12080fc2858ccc10b3b78bacc.png?quality=75&type=webp&imageView&thumbnail=160x160" mode=""></image>
				</div>
			</div>
		</div>
		<div class="freshman">
			<div class="man">
				<span class="line"></span>
				<span>新人专享礼</span>
				<span class="line"></span>
			</div>
			<div class="content clearfix">
				<a href="" class="left">
					<span>新人专享红包</span>
					<image src="https://yanxuan.nosdn.127.net/ba4d635ec94ad95b28bfab6500900659.png" mode=""></image>
				</a>
				<div class="right">
					<a href="" class="model1">
						<span>福利社</span>
						<p>今日特价</p>
						<image src="https://yanxuan-item.nosdn.127.net/31ccd16c627df7caab7179c789b7d7dc.png?quality=75&type=webp&imageView&thumbnail=200x200" mode=""></image>
					</a>
					<a href="" class="model2">
						<span>新人拼团</span>
						<p>1元起包邮</p>
						<image src="https://yanxuan-item.nosdn.127.net/bb9025c24057dfb89403055ac5b9f85c.png?quality=75&type=webp&imageView&thumbnail=200x200" mode=""></image>
					</a>
				</div>
			</div>
		</div>
		<div class="popular clearfix">
			<div class="title clearfix">
				<p>人气推荐</p>
				<a class="btn" @click="tuijian">更多<i class="iconfont icon-jiantou "></i></a>
			</div>
				<div class="more">
					<div class="spItem clearfix">
						<image src="https://yanxuan-item.nosdn.127.net/2b31ee5002606f7f9081738e9fb8bd5a.png?quality=75&type=webp&imageView&thumbnail=280x280" mode=""></image>
					</div>
					<div class="two clearfix">
						<span class="sp">年货特惠</span>
						<span class="sp">2件减10</span>
						<span class="qiyan">祺宴 尊享坚果礼盒 800克...</span>
						<span class="yingji">应季新货，雅致高端</span>
						<span class="prise">￥239</span>
					</div>		
				</div>
				<div class="m-goodGrid">
					<div class="shell">
						<div class="item">
							<image src="https://yanxuan-item.nosdn.127.net/9a33f08a3b0f5c06fdf4c586d51b2f7c.png?type=webp&imageView&quality=65&thumbnail=330x330" mode=""></image>
						</div>
					<span>全棉针织条纹四件套</span>
						<p>￥299</p> 
					</div >
					<div class="shell">
						<div class="item">
							<image src="https://yanxuan-item.nosdn.127.net/c0b3d87a8066b33c68294ce60f8e1920.png?type=webp&imageView&quality=65&thumbnail=330x330" mode=""></image>
						</div>
						<span>每一口都有七种鱼，全价猫粮...</span>
						<p>￥88</p> 
						<span class="sp">2件减10</span>
					</div>
					<div class="shell">
						<div class="item">
							<image src="https://yanxuan-item.nosdn.127.net/0434f5cb29b2c6c6ade2f1c0487ae97c.png?type=webp&imageView&quality=65&thumbnail=330x330" mode=""></image>
						</div>
						<span>泡脚不用倒水擦脚啦！蒸汽沐...</span>
						<p>￥449</p> 
					</div>
				</div>
		</div>
		<div class="popular clearfix">
				<div class="title clearfix">
					<p>限时购</p>
					<a class="btn">更多<i class="iconfont icon-jiantou "></i></a>
				</div>
					<div class="more">
						<div class="spItem clearfix">
							<image src="https://yanxuan-item.nosdn.127.net/2b31ee5002606f7f9081738e9fb8bd5a.png?quality=75&type=webp&imageView&thumbnail=280x280" mode=""></image>
						</div>
						<div class="two clearfix">
							<span class="sp">年货特惠</span>
							<span class="sp">2件减10</span>
							<span class="qiyan">祺宴 尊享坚果礼盒 800克...</span>
							<span class="yingji">应季新货，雅致高端</span>
							<span class="prise">￥239</span>
						</div>		
					</div>
					<div class="m-goodGrid">
						<div class="shell">
							<div class="item">
								<image src="https://yanxuan-item.nosdn.127.net/85b1bd60c128affe100068ed20037787.png?quality=75&type=webp&imageView&thumbnail=216x216" mode=""></image>
							</div>
							<p>￥199</p> 
						</div >
						<div class="shell">
							<div class="item">
								<image src="https://yanxuan-item.nosdn.127.net/7c850ef50fc408c4eab4d7abdb920da3.png?quality=75&type=webp&imageView&thumbnail=216x216" mode=""></image>
							</div>
							<p>￥1179</p> 
						</div>
						<div class="shell">
							<div class="item">
								<image src="https://yanxuan-item.nosdn.127.net/ab098b429e5a1f9715d938cd7d54f26a.png?quality=75&type=webp&imageView&thumbnail=216x216" mode=""></image>
							</div>
							<p>￥989</p> 
						</div>
					</div>
			</div>
		<div class="popular clearfix">
				<div class="title clearfix">
					<p>新品首发</p>
					<a class="btn" @click="xinpinshoufa()">更多<i class="iconfont icon-jiantou "></i></a>
				</div>
					<div class="more">
						<div class="spItem clearfix">
							<image src="https://yanxuan-item.nosdn.127.net/2b31ee5002606f7f9081738e9fb8bd5a.png?quality=75&type=webp&imageView&thumbnail=280x280" mode=""></image>
						</div>
						<div class="two clearfix">
							<span class="sp">年货特惠</span>
							<span class="sp">2件减10</span>
							<span class="qiyan">祺宴 尊享坚果礼盒 800克...</span>
							<span class="yingji">应季新货，雅致高端</span>
							<span class="prise">￥239</span>
						</div>		
					</div>
					<div class="m-goodGrid">
						<div class="shell">
							<div class="item">
								<image src="https://yanxuan-item.nosdn.127.net/9a33f08a3b0f5c06fdf4c586d51b2f7c.png?type=webp&imageView&quality=65&thumbnail=330x330" mode=""></image>
							</div>
						<span>全棉针织条纹四件套</span>
							<p>￥299</p> 
						</div >
						<div class="shell">
							<div class="item">
								<image src="https://yanxuan-item.nosdn.127.net/c0b3d87a8066b33c68294ce60f8e1920.png?type=webp&imageView&quality=65&thumbnail=330x330" mode=""></image>
							</div>
							<span>每一口都有七种鱼，全价猫粮...</span>
							<p>￥88</p> 
							<span class="sp">2件减10</span>
						</div>
						<div class="shell">
							<div class="item">
								<image src="https://yanxuan-item.nosdn.127.net/0434f5cb29b2c6c6ade2f1c0487ae97c.png?type=webp&imageView&quality=65&thumbnail=330x330" mode=""></image>
							</div>
							<span>泡脚不用倒水擦脚啦！蒸汽沐...</span>
							<p>￥449</p> 
						</div>
					</div>
			</div>
	</div>
</template>

<script>

	export default {
		
		data() {
			return {
				isshow:false,
				show:false,
				rotate:false,
				navIndex: 0,
				indexDatas: {},
				navList: [
					'推荐',
					'居家生活',
					'服饰鞋包',
					'美食酒水',
					'个护清洁',
					'母婴亲子',
					'运动旅行',
					'数码家电',
					'全球特色',
				],
				iconList:
					[
						{img:"https://yanxuan.nosdn.127.net/c6fd8835a6400b7da7a016ad85506b69.png",
							p:"新品首发",
						},
						{
							img:"https://yanxuan.nosdn.127.net/fede8b110c502ec5799702d5ec824792.png",
							p:"居家生活",
						},
						{
							img:"https://yanxuan.nosdn.127.net/896a3beac514ae8f40aafe028e5fec56.png",
							p:"服饰箱包",
						},
						{
							img:"https://yanxuan.nosdn.127.net/37520d1204a0c55474021b43dac2a69e.png",
							p:"美食酒水",
						},
						{
							img:"https://yanxuan.nosdn.127.net/6c3bd9d885c818b1f73e497335a68b47.png",
							p:"个护清洁",
						},
						{
							img:"https://yanxuan.nosdn.127.net/559d2a240ec20b096590a902217009ff.png",
							p:"母婴亲子",
						},
						{
							img:"https://yanxuan.nosdn.127.net/5c088559ebcc3f0ffcda663f04dfbeb2.png",
							p:"运动旅行",
						},
						{
							img:"https://yanxuan.nosdn.127.net/fbca8e1f2948f0c09fc7672c2c125384.png",
							p:"数码家电",
						},
						{
							img:"https://yanxuan.nosdn.127.net/f7281169d4e82d5d8d52aa1fec83fe01.png",
							p:"全球特色",
						},
						{
							img:"https://yanxuan.nosdn.127.net/12e8efd15b9b210ab156a7ee9b340548.gif",
							p:"好货抄底",
						}
					],
			}
		},
		methods: {
			changeNavIndex(index){
				this.navIndex = index
			},
			start(){
				this.rotate = !this.rotate
				this.show = !this.show
				this.isshow = !this.isshow
			},
			xinpinshoufa(){
					uni.redirectTo({
							url: '/pages/xinpinshoufa/xinpinshoufa'
					});
			},
			tuijian(){
					uni.redirectTo({
							url: '/pages/tuijian/tuijian'
					});
			}
		}
	}
</script>

<style lang="stylus">
	.index
		.header
			position fixed
			top 0
			left 0
			display flex
			padding 10upx
			background-color white
			z-index 99
			padding-top 20upx
			image
				width 140upx
				height 40upx
				margin 10upx 20upx
			.search
				width 440upx
				height 60upx
				background #eee
				border-radius 10upx
				line-height 60upx
				position relative
				.iconfont
					position absolute
					font-size 28upx
					left 30upx
				.input
					position absolute
					font-size 28upx
					color #666
					left 60upx
			button	
				width 100upx
				height 50upx
				font-size 16upx
				line-height 50upx
				text-align center
				margin-top 5upx
				margin-left 15upx
				color #DD1A21
				border 1upx #DD1A21 solid
				background none
		.scrollContainer
			position fixed
			top 85upx
			left 0
			z-index 99
			white-space nowrap
			background white
			.scrollItem 
				display inline-block
				margin 0 20upx
				width 140upx
				height 80upx
				text-align center
				line-height 80upx
				font-size 26upx
				&.active
					border-bottom 1upx solid #D43C33
			.down
				position fixed
				width 80upx
				height 50upx
				top 90upx
				left 680upx
				line-height 50upx
				text-align center
				z-index 999
				background white
				.go
					transform rotate(180deg)
				span
					display block
					transition all 800ms
					margin-top 10upx
					.icon-jiantou
						transform-origin:50% 50%
			.mask
				width 100%
				position fixed
				background white
				top 80upx
				z-index 99
				.all
					padding 30upx
					margin-left 10upx
					display flex
					justify-content space-between
					flex-wrap wrap
					p
						display block
						width 100%
						margin-bottom 20upx
					span
						display block
						width 160upx
						height 60upx
						border 2upx solid #ccc
						font-size 25upx
						line-height 60upx
						text-align center
						margin 10upx 0upx
						background #FAFAFA			
		swiper
			margin-top 160upx
			width 100%
			height 370upx
			image
				width 100%
				height 370upx
		.m-index
			display flex
			justify-content space-between
			margin 30upx 0
			ul
				width 100%
				margin-left 7%
				vertical-align middle
				li
					display block
					float left
					width 33%
					line-height 100%	
					image
						width 40upx
						height 40upx
						float left
					p
						margin-top 5upx
						font-size 22upx
		.icon-all
			width 100%
			padding 20upx
			display flex
			flex-wrap wrap
			.icon
				text-align center
				width 20%
				image
					display block
					width 110upx
					height 110upx
					float left
				p
					display block
					font-size 30upx
					float left
					margin 10upx 0
		.advertisement
			width 100%
			background #ffecd7
		.goods
			.out
				width 100%
				height 250upx
			.in
				position absolute
				top 1020upx
				left 70upx
				width 180upx
				height 180upx
			.prise
				font-size 20upx
				color white
				width 80upx
				height 30upx
				background #F48F18
				text-align center
				line-height 30upx
				border-radius 20upx
				position absolute
				left 115upx
				bottom -90upx
		.proItem
			width 100%
			padding 5% 5% 2% 5% 
			image
				width 90%
				height 80upx
		.floor
			position relative
			width 90%
			margin 0 5%
			display flex
			justify-content space-between
			flex-wrap wrap
		 .clearfix::before,
		 .clearfix::after
				content: '';
				display: table;
				clear: both;   
			a
				width 48%
				.img1
					position absolute
					width 325upx
					height 180upx
				.img2
					position absolute
					width 150upx
					height 150upx
				.img2_1
					left 180upx
				.img2_2
					left 545upx
		.vip
			width 100%
			image
				width 90%
				height 150upx
				margin 190upx 0 1% 5%
		.new_year
				width 100%
				image
					width 100%
					height 80upx
		.four
			width 90%
			margin-left 5%
			display flex
			justify-content space-between
			flex-wrap wrap
			.bac
				width 160upx
				height 190upx
				background url("https://yanxuan.nosdn.127.net/366b61d60442c1d9121e9d54534b53b8.png?quality=75&type=webp&imageView&thumbnail=188x0")
				background-size 100% 100%
				text-align center
				margin-bottom 20upx
				title
					color #FFFFFF
					font-size 25upx
					font-weight bold
				p
					font-size 20upx
					color #FFFFFF
				.promGoods
					width 150upx
					height 130upx
		.freshman
			background #FFFFFF
			border-top 20upx solid #EEEEEE
			border-bottom 20upx solid #EEEEEE
			height 520upx
			.man
				padding 20upx
				width 100%
				text-align center
			.line
				display inline-block
				background black
				width 30upx
				height 2upx
				margin 0 10upx 10upx 10upx
		.content
			margin-left 5%
			margin-right 3%
			.left
				float left
				width 47%
				height 400upx
				background #F9E9CF
				padding-top 20upx
				span
					display block
					margin 20upx 0 10upx 20upx
				image
					width 80%
					height 280upx
					margin-left 10%
					margin-top 20upx
			.right
				width 47%
				height 400upx
				float left
				margin-left 10upx
				.model1
					width 100%
					height 50%
					background #FBE2D3
					padding 20upx 0 0 20upx
					span
						font-size 30upx
					p
						font-size 20upx
						color #7F7F7F
					image
						width 195upx
						height 200upx
						margin-left 150upx
						margin-top -55upx
				.model2
					width 100%
					height 170upx
					background #FFECC2
					padding 20upx 0 0 20upx
					margin-top 10upx
					span
						font-size 30upx
					p
						display block
						background #CBB693
						font-size 20upx
						color #FFFFFF
						width 95upx
						margin-left 10upx
					image
						width 195upx
						height 200upx
						margin-left 150upx
						margin-top -55upx
		.popular
			width 100%
			padding 30upx
			border-bottom 20upx #eee solid
			.title
				p
					font-size 30upx
					float left
				.btn
					width 125upx
					height 50upx
					float right
					font-size 25upx
					margin-right 40upx
					i
						font-size 25upx
						float right
						margin-right 40upx
						margin-top 5upx
						transform-origin:50% 50%
			.more
				display flex
				background #FEF0DF
				width 92%
				.spItem
					image
						width 300upx
						height 300upx
				.two
					width 50%
					.sp
						font-size 20upx
						background #FFFFFF
						display block
						float left
						width 100upx
						height 30upx
						color #DD1A21
						border 1upx solid #DD1A21
						border-radius 20upx
						margin 60upx 10upx 0 0
						text-align center
						line-height 30upx
					.qiyan
						padding-top 110upx
						display block
						font-size 30upx
						width 370upx
					.yingji
						font-size 27upx
						color #7F7F7F
			.m-goodGrid		
				width 92%
				display flex
				justify-content space-between
				flex-wrap wrap
				margin-top 20upx
				.shell
					width 33%
					.item
						width 220upx
						height 225upx
						background #f5f5f5
						float left
						image
							width 225upx
							height 210upx
					span
						font-size 25upx
					p
						color #DD1A21
					.sp
						font-size 20upx
						background #FFFFFF
						display block
						float left
						width 100upx
						height 30upx
						color #DD1A21
						border 1upx solid #DD1A21
						border-radius 20upx
						text-align center
						line-height 30upx
		</style>
