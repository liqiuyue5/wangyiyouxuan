<template>
	<div class="detailContainer" @touchmove="touchStart">
		<div class="img">
			<image src="https://yanxuan.nosdn.127.net/3137220cc522a8fbb0b7520637a61469.png" mode=""></image>
		</div>
		<!-- 网易严选头部 -->
		<div class="detailTop">
			<span class="iconfont icon-Homehomepagemenu"></span>
			<span>网易严选</span>
			<div class="detailRight">
				<span class="iconfont icon-search2"></span>
				<span class="iconfont icon-Shoppingcart"></span>
			</div>
		</div>
		<!-- 轮播图 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item>
				<image :src="backData.detailById.itemDetail.picUrl3" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image :src="backData.detailById.itemDetail.picUrl4" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image :src="backData.detailById.itemDetail.picUrl1" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image :src="backData.detailById.itemDetail.picUrl2" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://yanxuan.nosdn.127.net/d8645b184bb0b7c9e471d9212d283939.jpg" mode=""></image>
			</swiper-item>
		</swiper>
		<!-- 轮播图下面 -->
		<div class="info">
			<image src="https://yanxuan.nosdn.127.net/83516d73ecd395749e0f4b59176b0b10.png"></image>
			<div class="infoPrice">
				<p>{{backData.detailById.specialPromTag}}</p>
				<span class="infoNewPrice">${{backData.detailById.retailPrice}}</span>
				<span class="infoOldPrice">${{backData.detailById.counterPrice}}</span>
			</div>
			<span class="being">正在抢购中</span>
		</div>
		<!-- 推荐理由 好评率 -->
		<div class="radeRecommend">
			<div class="rate">
				<div class="rateLeft">
					<p class="rateLeftOne">{{backData.detailById.comments[0].itemName}}</p>
					<p class="rateLeftTwo">推荐理由</p>
				</div>
				<i class="iconfont icon-arrow-right-copy-copy"></i>
				<div class="rateRight">
					<p class="rateRightOne">{{backData.detailById.goodCmtRate}}</p>
					<p class="rateRightTwo">好评率</p>
				</div>
			</div>
			<!-- 推荐理由 -->
			<div class="recommend">
				<p class="recommendOne" v-for="(item,index) in backData.detailById.recommendReason" :key="index">
					<span class="number">{{index+1}}</span>
					<span class="benefits">{{item}}</span>
				</p>
				
		</div>
		<!-- 购物返 -->
		<div class="tradBack">
			<div class="tradBackLeft"> 
				<span>{{backData.detailById.shoppingReward.name}}:{{backData.detailById.shoppingReward.rewardDesc}}</span>
				<span class="integral">{{backData.detailById.shoppingReward.rewardValue}}</span>
			</div>
			<span class="iconfont icon-arrow-right-copy-copy"></span>
		</div>
		<div class="amount">
			<span>请选择规则数量</span>
			<span class="iconfont icon-arrow-right-copy-copy"></span>
		</div>
		<div class="limit">
			<p>限制：{{backData.detailById.itemLimit}}</p>
		</div>
		<div class="amount">
			<span>配送：请选择配送地址</span>
			<span class="iconfont icon-arrow-right-copy-copy"></span>
		</div>
		<div class="serve">
			<div class="serveMany">
				<span class="serveText">服务：</span>
				<ul>
					<li v-for="(item,index) in backData.detailById.policyList" :key="index"><a href="javascript:;">{{item.title}}</a></li>
					<!-- <li><a href="javascript:;">48小时快速退款</a></li>
					<li><a href="javascript:;">满88元免邮费</a></li>
					<li><a href="javascript:;">国内部分地区无法配送</a></li>
					<li><a href="javascript:;">不支持红包支付</a></li>
					<li><a href="javascript:;">不享受企业特权</a></li>
					<li><a href="javascript:;">不享受学生特权</a></li>
					<li><a href="javascript:;">不支持回馈金抵扣</a></li> -->
				</ul>
				<span class="iconfont icon-arrow-right-copy-copy"></span>
			</div>
		</div>
		<image src="https://yanxuan.nosdn.127.net/be23cd60441629e9070bc50219414c8f.png" mode=""></image>
		<div class="userSpeack">
			<span class="userEvaluation">用户评价(851)</span>
			<div class="rateOf">
				<span class="accounted">{{backData.detailById.goodCmtRate}}</span>
				<span class="betterAccounted">好评率</span>
				<span class="iconfont icon-arrow-right-copy-copy"></span>
			</div>
		</div>
		</div>
		<!-- 回到顶部 -->
		<div class="backTop" v-show="isShow">
			<span class="iconfont icon-jiantouxiangshang"></span>
		</div>
		<!-- 底部固定部分 -->
		<div class="fixation">
			<div>
				<span class="iconfont icon-erji"></span>
				<span class="quickShop">立即购买</span>
				<span class="addCar" @click="addShoppingCar">加入购物车</span>
			</div>
		</div>
	</div>
</template>

<script>
	import request from '../../utils/request.js'
	const app = getApp()
	// app.$vm.test
	export default{
		data(){
			return {
				canlog:true,
				isShow:false,//默认显示回到顶部
				backData:{},
				id:0
			}
		},
		async mounted(){
			this.id = app.$vm.id
			console.log(this.id)
			// this.$event.$on("getDetail",(id)=>{
			// 	console.log("11")
			// 	this.id=id
			// })
			let backData=await request("/detail?id="+this.id)
			console.log(backData)
			this.backData=backData
		},
		methods:{
			// 节流
			touchStart(){
				if(this.canlog){
					console.log("111")
					this.canlog=false
					setTimeout(()=>{
						this.canlog=true
					},1000)	
					console.log()
				}
			},
			onPageScroll (res){
				if(res.scrollTop>200){
					this.isShow=true
				}else{
					this.isShow=false
				}
			},
			// 添加到购物车
			 async addShoppingCar(){
				// 如果当前购物车中有该物品时，只要添加数据即可
				let carData = app.$vm.checked.filter((item)=>{
					return item.cartItemList[0].itemId==this.id
				})
				console.log(carData)
				if(carData.length){
					console.log(carData.length)
					carData.forEach((item,index)=>{
						item.cartItemList[0].cnt++
					})
				}else{
					// let addElseData=await request("/detail?id="+this.id)
					// app.$vm.checked.unshift()
				}
				// 如果没有此类商品时
				// 传过来这个物品的id
				
				wx.showToast({
				  title: '加入成功',
				  icon: 'none',
				  duration: 2000
				})
			}
		}
		
	}
</script>

<style lang="stylus">
	.detailContainer
		width 100%
		.img
			image
				width 100%
				height 104upx
		.detailTop 
			width 100%
			display flex
			padding 0 24upx
			box-sizing border-box
			z-index 50
			background-color white
			span
				flex 33.33%
				display inline-block
			.icon-Homehomepagemenu
				font-size 60upx
			.detailRight 
				display inline-block
				span 
					font-size 60upx
		swiper
			height 750upx
			width 100%
			image
				width 100%
				height 750upx
		.info
			background-color #DD1A21
			image
				width 106upx
				height 106upx
				vertical-align middle
			.infoPrice
				display inline-block
				color #FFFFFF
				border-left #F48F18 1upx solid
				width 459upx
				vertical-align middle
				p
					font-size 23upx
					margin 12upx 0 0 12upx
				.infoNewPrice 
					font-size 46upx
					margin-left 12upx
				.infoOldPrice
					font-size 23upx
					text-decoration line-through
					margin-left 10upx
			.being  
				font-size 23upx
				color #FFFFFF
		.radeRecommend
			.rate	
				width 100%
				padding 20upx
				box-sizing border-box
				background-color #FFFFFF
				&:after
					content ""
					display block
					clear both
				.rateLeft
					float left
					.rateLeftOne
						color #333333
						font-size 32upx
						height 48upx
						line-height 48upx
					.rateLeftTwo
						color #333333
						font-size 24upx
						height 36upx
						line-height 36upx
				.rateRight	
					float right
					vertical-align middle
					.rateRightOne
						color #333333
						font-size 32upx
						height 48upx
						line-height 48upx
					.rateRightTwo
						color #333333
						font-size 24upx
						height 36upx
						line-height 36upx
				.icon-arrow-right-copy-copy
					float right
					vertical-align bottom
					height 72upx
					line-height 72upx
			.recommend	
				padding 14upx 40upx
				background-color #FFFFFF
				border 2upx solid #EEEEEE
				box-sizing border-box
				.recommendOne
					.number 
						border 1upx solid #DD1A21
						font-size 24upx
						border-radius 50%
						width 24upx
						height 24upx
						line-height 24upx
						display inline-block
						text-align center
						margin-right 10upx
					.benefits
						font-size 24upx
						color #333333
			.tradBack	
				display flex
				justify-content space-between
				margin-top 20upx
				padding 20upx
				background-color #FFFFFF
				box-sizing border-box
				.tradBackLeft
					span 
						color #333333
						font-size 28upx
					.integral
						color #DD1A21
				.icon-arrow-right-copy-copy	
					margin-top 10upx
			.amount	
				display flex
				justify-content space-between
				padding 32upx 20upx
				border-bottom 2upx solid #EEEEEE
				background-color #FFFFFF
				margin-top 10upx 
				span
					font-size 28upx
			.limit	
				padding 32upx 20upx
				background-color #FFFFFF
				p
					font-size 28upx
			.serve	
				margin-bottom 20upx
				background-color #FFFFFF
				.serveMany
					display flex
					justify-content space-between
					padding 0 20upx
					.serveText
						display inline-block
						color #333333
						font-size 28upx
					ul
						li
							list-style-type disc
							color #7F7F7F
							font-size 28upx
							margin 0 40upx 16upx 0
							padding 0 0 0 16upx
							display inline-block
					.icon-arrow-right-copy-copy
						vertical-align middle
			image
				width 100%
				height 200upx
			.userSpeack	
				display flex
				justify-content space-between
				padding 0 20upx
				margin-bottom 100upx
				background-color #FFFFFF
				.userEvaluation
					font-size 28upx 
					color #333333
					margin-top 12rpx
				.rateOf
					.accounted
						color #DD1A21
						font-size 28upx
					.betterAccounted	
						font-size 28upx
						color #333333
					.icon-arrow-right-copy-copy
						font-size 28upx
		.backTop
			position fixed
			width 82upx
			height 82upx
			background-color #FFFFFF
			color #333333
			border-radius 50%
			line-height 82upx
			text-align center
			font-size 28upx
			border 1px solid #EEEEEE
			right 20upx
			visibility visible
			bottom 400upx
		.fixation	
			position fixed
			bottom 0
			width 100%
			height 104upx
			background-color #FFFFFF
			.icon-erji
				width 156upx
				height 104upx
				line-height 104upx
				display inline-block
				font-size 50upx
				text-align center
				border-right 1upx solid #EEEEEE
			.quickShop	
				font-size 28upx
				width 297upx
				height 104upx
				line-height 104upx
				text-align center
				display inline-block
			.addCar
				display inline-block
				color #FFFFFF
				background-color #DD1A21
				width 297upx
				height 104upx
				line-height 104upx
				text-align center
				font-size 28upx
</style>
