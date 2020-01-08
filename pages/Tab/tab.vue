<template>
	<div>
		
			<div class='header-container'>
					<div class="top">
						<div class="home">
							<image src="../../static/imgs/icon.webp"></image>
						</div>
						<div class="input-contaier" @click="toSearch">
							<div class='sousuo'>
								<image src="../../static/imgs/icon.webp"></image>
							</div>
							<div class='del' @click="empty">x</div>
							<input type="text" value="保暖内衣"/>
						</div>
					</div>
					<div class="bottom">
						<div>综合</div>
						<div class='price' @click='price()'>
							价格
							<image src="../../static/imgs/sx.webp"></image>
						</div>
						<div>分类</div>
					</div>
					
				</div>
			
		
		<div class='tab-container'>
			<div class="commodity-list">
				<div class="commodity-item" v-for="(item,index) in itemList" :key="index">
					<image :src="item.scenePicUrl"></image>
					<span class="title">{{item.name}}</span>
					<span class='money'>￥{{item.counterPrice}}</span>
					<span class='sign'>年货特惠</span>
				</div>
			</div>
		</div>
		
	</div>
	</template>

<script>
	
	import config from '../../utils/config.js'
	export default{
		methods:{
			empty(){
				wx.navigateTo({
					url:'../../pages/Search/search'
				})
			},
			toSearch(){
				wx.navigateTo({
					url:'../../pages/Search/search'
				})
				this.isShow=false
				console.log(this.isShow)
			},
			price(){
				this.flag = !this.flag
				if(this.flag){
					
				}
			}
		},
		data(){
			return{
				itemList:[],
				flag:true
			}
		},
		
		onLoad() {
			wx.request({
				url:'http://localhost:3000/tab',
				success:(res)=>{
					console.log(res.data.itemList)
					this.itemList = res.data.itemList
				}
			})
		}
	}
</script>

<style lang="stylus" scoped>
	.header-container
			width 100%
			display fixed
			top 0 
			left 0
			.top
				padding 20upx 30upx
				display flex
				.input-contaier
					position relative
					.sousuo
						position absolute
						left 10upx
						overflow hidden
						width 100upx
						height 50upx
						image
							width 100upx
							height 350upx
							transform translateY(-295upx)
					.del
						position absolute
						background #C8D0CA
						color #E9EAEA
						top 15upx
						right 20upx
						border-radius 50%
						font-size 30upx
						width 30upx
						height 30upx
						text-align center
						line-height 21upx
					input
						background #F4F4F4
						color #333
						font-size 30upx
						padding-left 60upx
						border-radius 5upx
						width 500upx
				.home 
					width 70upx
					height 60upx
					overflow hidden
					image
						width 180upx
						height 450upx
						transform translateY(-77upx)
			.bottom
				display flex
				justify-content space-between
				background #FAFAFA
				height 100upx
				div
					width 33.3%
					text-align center
					line-height 100upx
					font-size 35upx
				.price
					position relative
					image
						width 17upx
						height 25upx
						position absolute
						top 40upx
						right 70upx

	
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
					font-size 30upx
					line-height 1.2
				.money
					color #E44B51
					font-size 30upx
				.sign
					border-radius 30upx
					border 1upx solid #E96C70
					font-size 20upx
					color #E96C70
					padding  3upx 5upx 5upx 5upx
					width 80upx
					line-height 100%
</style>
