<template>
	<view class="search-container">
		<div class="search-content">
			<div class="header">
				<input type="text" value="送礼佳品 即食燕窝">
					<i class='iconfont icon-sousuo'></i>
				</input>
				<div class='sousuo'>
					<image src="../../static/imgs/icon.webp"></image>
				</div>
				<a href="">取消</a>
			</div>
			<div class="tab-container" v-show="isShow">
				<div class="hot">热门搜索</div>
				<div class="tab-list">
					<a href="">美食99选9</a>
					<a href="">爆品秒杀低至0.1元</a>
					<a href="" @click="toTabweb(id)">年货礼盒</a>
					<a href="" @click="toTabweb(id)">保暖内衣</a>
					<a href="" @click="toTabweb(id)">网红足浴盆</a>
					<a href="" @click="toTabweb(id)">冬季收纳</a>
					<a href="" @click="toTabweb(id)">羽绒服</a>
					<a href="" @click="toTabweb(id)">无骨凤爪</a>
					<a href="" @click="toTabweb(id)">羽绒服女</a>
					<a href="" @click="toTabweb(id)">锅</a>
					<a href="" @click="toTabweb(id)">杯子</a>
					<a href="" @click="toTabweb(id)">收纳</a>
				</div>
			</div>
		</div>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isShow:true
			}
		},
		methods: {
			toTabweb(id){
				wx.navigateTo({
					url:'../Tab/tab'
				})
			}
		}
	}
</script>

<style lang="stylus" scoped>
	.search-container
		width 100%
		background #EEEEEE
		.search-content
			width 100%
			background white
			padding 10upx 30upx
			box-sizing border-box
			.header
				display flex
				justify-content space-between
				font-size 30upx
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
				input
					background #F4F4F4
					color #AAAAAA
					width 550upx
					padding-left 50upx
				a
					padding-top 10upx
			.tab-container
				margin-top 30upx
				.hot
					font-size 35upx
					color #999
					margin 10upx 0
				.tab-list
					a
						border 1upx #D7D7D7 solid
						color #333
						font-size 24upx
						display inline-block
						padding  5upx 10upx
						margin 0 25upx 25upx 0
</style>
