<template>
	<!-- 购物车 -->
	<div class="carContainer">
		<!-- 购物车容器没登录时  v-show-->
		<div class="shoppingCar"  v-show="localStorage">
			<!-- 购物车头部 -->
			<div class="shoppingTop">
				<image src="https://yanxuan.nosdn.127.net/3137220cc522a8fbb0b7520637a61469.png" mode=""></image>
			</div>
			<div class="redemption">
				<span class="spanLeft">购物车</span>
				<span class="spanRight">领券</span>
			</div>
			<ul class="list">
				<li><span class="iconfont icon-yuan"></span><a href="javascript:;">30天无忧退货</a></li>
				<li><span class="iconfont icon-yuan"></span><a href="javascript:;">48小时快速退款</a></li>
				<li><span class="iconfont icon-yuan"></span><a href="javascript:;">满88元免邮费</a></li>
			</ul>
			<div class="center">
				<div class="add">
					<i class='iconfont icon-Shoppingcart'>购物车图标</i>
					<div class="toLogin">
						<p>去添加点什么吧</p>
						<span>登录</span>
					</div>
				</div>
			</div>
		</div>
		<!-- 购物车容器登录时 v-show -->
		<div class="shoppingCarLogin">
			<div class="shoppingLoginTop">
				<image src="https://yanxuan.nosdn.127.net/3137220cc522a8fbb0b7520637a61469.png"></image>
			</div>
			<div class="exit">
				<span class="exitShopCar">购物车</span>
				<div class="exitRight">
					<span class="coupon">领券</span>
					<span class="exiting">编辑</span>
				</div>
			</div>
			<ul class="ulList" v-if="sunMoney==0">
				<li><a href="javascript:;">30天无忧退货</a></li>
				<li><a href="javascript:;">48小时快速退款</a></li>
				<li><a href="javascript:;">满88元免邮费</a></li>
			</ul>
			<div class="packageMail" v-if="sunMoney>=88">
				<p>已满足包邮条件</p>
			</div>
			<a class="noPackageMail" v-if="sunMoney<88&&sunMoney>0">
				<sapn class="coudan">再购${{sunMoney}}免邮,去凑单<span class="iconfont icon-arrow-right-copy-copy"></span></sapn>
				<span class="iconfont icon-arrow-right-copy-copy"></span>
			</a>
			<!-- 购物车列表 -->
			<div class="shops" v-for="(item,index) in checked" :key="index">
				<div class="shopsLeft">
					<i class="iconfont" @click="changeIcon(index)" :class="item.checked?'icon-checked':'icon-unchecked'"></i>
				</div>
				<div class="shopsRight">
					<div class="shopsRightTop" v-if="item.cartItemList[0].timingPromotion">
						<span class="snapUp">{{item.cartItemList[0].timingPromotion}}</span>
						<span class="countdown">{{item.cartItemList[0].finishTip}}11天10小时</span>
					</div>
					<div class="shopRightBot">
						<image @click="skip(index)" :src="item.cartItemList[0].pic" mode=""></image>
						<div class="introduce">
							<div class="introduceList">
								<span class="goodThings">好货内部价</span>
								<span class="cargo">{{item.cartItemList[0].itemName}}</span>
							</div>
							<div class="type">
								<span class="kind" v-for="(kind,indexTow) in item.cartItemList[0].specList" :key="indexTow">{{kind.specValue}}</span>
								<span class="iconfont icon-jiantou"></span>
							</div>
							<div class="price">
								<span class="presentPrice">{{item.cartItemList[0].actualPrice}}</span>
								<span class="originalPrice">{{item.cartItemList[0].retailPrice}}</span>
								<div class="quantity">
									<span class="reduction" @click="reduction(index)">-</span>
									<span>{{item.cartItemList[0].cnt}}</span>
									<span class="append" @click="append(index)">+</span>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<!-- 下单 -->
		<div class="order">
			<div class="orderLeft">
				<span class="iconfont" @click="allChecked" :class="index?'icon-checked':'icon-unchecked'"></span>
				<span>已选({{checkNumber}})</span>
			</div>
			<div class="orderRight">
				<div class="combined">
					<p class="combinedPrice">合计:{{sunMoney}}</p>
					<p class="preferential" v-if="space">已优惠:{{space}}</p>
				</div>
				<span class="placeTheOrder" :class="{active:checkNumber>0}">下单</span>
			</div>
		</div>
	</div>
</template>

<script>
	import request from '../../utils/request.js'
	const app = getApp()
	// const getId = app.$vm.getId
	export default {
		data() {
			return {
				localStorage:"",//看localStroge中是否存在token,根据是否登录展示不同的页面
				sum:0,//当前勾选商品的总数量
				index:false,//全选与全不选
				number:2, //当前挑选单个商品的数量
				sunMoney:0,//总价钱
				pricePread:0,
				// shops:[],//选择的商品数量
				checked:[],//购物车列表
				results:[],
				space:0,
				checkNumber:0//选中的个数
			}
		},
		computed:{
		},
		watch:{
			
		},
		onLoad() {
			// this.localStorage=localStorage.getItem.token_key
		},
		async mounted(){
			let result = await request('/shoppingCar')
			this.checked = result.data.cartGroupList
			
			// this.shops=result.data.cartGroupList.cartItemList
			console.log(this.checked)
			this.checked.forEach((item,index)=>{
				console.log(item.specList)
			})
		},
		methods: {
			// 跳到详情页
			skip(index){
				// this.$event.$emit("getDetail",this.checked[index].cartItemList[0].itemId)
				uni.$emit("getDetail",this.checked[index].cartItemList[0].itemId,this.checked)
				uni.navigateTo({
				    url: '/pages/details/details'
				});
			},
			filterChecked(){
				let resultChecked = this.checked.filter((item)=>{
					return item.checked
				})
				this.results=resultChecked
				this.checkNumber=this.results.length
				console.log(this.results)
				this.sunMoney=this.results.reduce((pre,item)=>{
					return pre+(item.cartItemList[0].actualPrice)*(item.cartItemList[0].cnt)
				},0)
				this.space=this.results.reduce((pre,itemTwo)=>{
					return pre+(itemTwo.cartItemList[0].retailPrice-itemTwo.cartItemList[0].actualPrice)*(itemTwo.cartItemList[0].cnt)
				},0)
				console.log(this.sunMoney)
			},
			// 点击按钮全选
			allChecked(){
				this.index=!this.index
				if(this.index){
					this.checked.forEach((item,index)=>{
						item.checked=true
						this.checkNumber=this.checked.length
						this.filterChecked()
					})
				}else{
					this.checked.forEach((item,index)=>{
						item.checked=false
						this.checkNumber=0
						this.filterChecked()
					})
				}
			},
			// 单个商品数据选中状态 总钱数以及优惠钱数
			changeIcon (index){
				this.checked[index].checked=!this.checked[index].checked
				console.log(this.checked[index])
				this.filterChecked()
				let resultChecked = this.checked.filter((item)=>{
					return item.checked==false
				})
				if(resultChecked.length>0){
					this.index=false
				}else{
					this.index=true
				}
			},
			// -
			reduction(index){
				// console.log(this.checked[index])
				if(this.checked[index].cartItemList[0].cnt<=1){
					wx.showToast({
					  title: '1件商品起售',
					  icon: 'none',
					  duration: 2000
					})
					return
				}else{
					this.checked[index].cartItemList[0].cnt--
					this.filterChecked()
				}
			},
			// +
			append(index){
				this.checked[index].cartItemList[0].cnt++
				this.filterChecked()
			},
			// 过滤选中的物品
			
		}
	}
</script>

<style lang="stylus">
	.carContainer		
		.shoppingCar			
			.shoppingTop				
				image					
					width 100%
					height 104upx
			.redemption
				display flex
				justify-content space-between
				padding 0 30upx
				.spanLeft
					font-size 36upx
				.spanRight
					font-size 30upx
			.list
				display flex 
				list-style-type square
				background-color white
				&:after
					content ""
					clear both
				li
					float left
					font-size 24upx
					flex 33.3333%
					text-align center
					height 70upx
					line-height 70upx
			.center	
				margin 0 auto
				.add
					.icon-Shoppingcart
						width 248upx
						height 248upx
					.toLogin	
						text-align center
						p
							font-size 28upx
							margin-bottom 50upx
						span
							display inline-block
							width 480upx
							height 92upx
							line-height 92upx
							background-color #DD1A21
							color white
							font-size 38upx
		.shoppingCarLogin
			.shoppingLoginTop
				image
					width 100%
					height 104upx		
			.exit
				display flex
				padding 0 30upx
				height 89upx
				line-height 89upx
				justify-content space-between
				.exitShopCar
					font-size 36upx
				.exitRight
					.coupon
						font-size 20upx
						background-color #FC865F
						padding 8upx 15upx
						color white
					.exiting
						font-size 30upx
						margin-left 30upx
			.ulList
				display flex
				list-style-type square
				background white
				&:after
					content ""
					clear both
				li
					float left
					font-size 24upx
					flex 33.3333%
					text-align center
					height 70upx
					line-height 70upx
			.packageMail	
				width 100%
				height 80upx
				line-height 80upx
				padding 0 30upx
				background-color #fff8d8
				box-sizing border-box
				p
					font-size 30upx
					color #F48F18
			.noPackageMail
				width 100%
				height 80upx
				line-height 80upx
				padding 0 30upx
				box-sizing border-box
				background-color #fff8d8
				display flex
				justify-content space-between
				.coudan
					font-size 30upx
					color #F48F18
					.icon-arrow-right-copy-copy
						font-size 30upx
				.icon-arrow-right-copy-copy	
					margin-right 50upx
					font-size 35upx
					color #F48F18
			.shops
				width 100%
				height 268upx
				background-color white
				&:last-child
					margin-bottom 100upx
				&:after
					display block
					content ""
					clear both
				.shopsLeft
					line-height 268upx
					float left
					margin-left 15upx
					.icon-checked
						color #DD1A21
				.shopsRight
					float left
					height 100%
					margin-left 20upx
					.shopsRightTop
						height 30upx
						line-height 30upx
						margin-top 20upx
						.snapUp
							border 1px solid #F48F18
							color #F48F18
							font-size 20upx
						.countdown
							font-size 22upx
							margin-left 20upx
				.shopRightBot	
					display flex
					padding 24upx 30upx 0 0
					justify-content space-between
					image
						width 172upx
						height 172upx
						margin-right 10upx
					.introduce
						.introduceList
							.goodThings
								font-size 28upx
								color #f48f18
							.cargo
								display inline-block
								font-size 28upx
								color #333333
								width 300upx
								overflow hidden
								white-space nowrap
								text-overflow ellipsis
								vertical-align middle
						.type	
							color #7F7F7F
							font-size 24upx
							height 38upx
							background-color #FAFAFA
							padding 0 10upx
							margin-top 10upx
							line-height 38upx
							display inline-block
							span
								vertical-align middle
						.price
							margin-top 24upx
							.presentPrice
								font-size 28upx
								color #333333
							.originalPrice
								font-size 24upx
								color #999999
								text-decoration line-through
								margin-left 10upx
							.quantity
								display inline-block
								margin-left 150upx
								span
									display inline-block
									border 1px solid #EEEEEE
									font-size 28upx
									width 58upx
									height 52upx
									text-align center
									line-height 52upx
									// align-items center
		.order	
			position fixed
			bottom 0upx
			width 100%
			height 96upx
			border-top 1px solid #EEEEEE
			border-bottom 1px solid #EEEEEE
			background-color #FFFFFF
			&:after
				display block
				content ""
				clear both
			.orderLeft
				color #7F7F7F
				font-size 20upx
				float left
				margin-left 15upx
				line-height 96upx
				.icon-checked
					color #DD1A21
				span
					vertical-align middle
			.orderRight	
				float right
				.combined
					display inline-block
					margin-right 20upx
					.combinedPrice
						color #DD1A21
						font-size 28upx
						margin-top 10upx
					.preferential
						color #7F7F7F
						font-size 22upx
				.placeTheOrder	
					width 256upx
					height 96upx
					background-color #cccccc
					display inline-block
					color #FFFFFF
					line-height 96upx
					text-align center
					vertical-align top
					&.active
						background-color #DD1A21
</style>
	