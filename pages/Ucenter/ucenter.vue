<template>
	<div class='ucenter-container'>
		<div class="top">
			<div class="header">
				<div class="avatar">
					<image class="userImg" :src="userInfo.avatarUrl?userInfo.avatarUrl:'../../static/images/personal/personal.png'" mode=""></image>
				</div>
				<div class="name">
					<span class="phone">{{userInfo.nickName?userInfo.nickName:'未登录'}}</span>
					<span class="level">{{userInfo.nickName?'微信用户':'点击登录账号'}}</span>
				</div>
				<image src="../../static/imgs/red.png" class="prize"></image>
				<div class="code">
					<image src="../../static/imgs/icon2.webp"></image>
				</div>
			</div>
			<div class="cardBag">
				<h2>我的资产</h2>
				<div class="card-list">
					<div class="card-item">
						<span>￥0</span>
						<span>回馈金</span>
					</div>
					<div class="card-item">
						<span>0</span>
						<span>红包</span>
					</div>
					<div class="card-item">
						<span>0</span>
						<span>优惠券</span>
					</div>
					<div class="card-item">
						<span>￥0</span>
						<span>津贴</span>
					</div>
					<div class="card-item">
						<span>0</span>
						<span>礼品卡</span>
					</div>
				</div>
			</div>
		</div>
		<div class="model">
			<div class="model-item" v-for="(item,index) in personalList" :key="index">
				<i class='iconfont' :class="item.icon"></i>
				<span>{{item.name}}</span>
			</div>
		</div>
		<div class="bottom" @click='logout()'>
			退出登录
		</div>
	</div>
</template>

<script>
	
	export default{
		data(){
			return{
				
				userInfo: {
					
				},
				personalList: [
					{
						name: '我的订单',
						icon: 'icon-dingdan'
					},
					{
						name: '周六一起拼',
						icon: 'icon-pintuandingdan'
					},
					{
						name: '领红包',
						icon: 'icon-sousuo'
					},
					{
						name: '我的积分',
						icon: 'icon-jifen'
					},
					{
						name: '地址管理',
						icon: 'icon-dizhiguanli'
					},
					{
						name: '账号安全',
						icon: 'icon-icon_anquan'
					},
					{
						name: '联系客服',
						icon: 'icon-kefu'
					},
					{
						name: '用户反馈',
						icon: 'icon-fankui'
					},
					{
						name: '帮助中心',
						icon: 'icon-bang_zhu_zhong_xin'
					},
					{
						name: '退还/售后',
						icon: 'icon-dingdan'
					},
					{
						name: '地址管理',
						icon: 'icon-dizhiguanli'
					}
				]
			}
		},
		mounted(){
			wx.getStorage({
				key:'isLogin',
				success(res) {
					console.log(res.data)
				},
				fail(err) {
					console.log('未登录')
					wx.reLaunch({
						url:'../Login/login'
					})
				}
			})
			console.log(this.$mp.query.userInfo)
			if(this.$mp.query.userInfo){
				let userInfo = JSON.parse(this.$mp.query.userInfo)
				this.userInfo = userInfo
			}else {
				wx.getUserInfo({
					success:(res) => {
						this.userInfo = res.userInfo
					},
					fail: () => {
						console.log('获取失败')
					}
				})
			}
		},
		methods: {
			toLogin(){
				if(this.userInfo.nickName){
					return
				}
				wx.navigateTo({
					url: '/pages/login/login'
				})
			},
			logout(){
				wx.clearStorage({
				key:'isLogin',
				success(res) {
					console.log('清除缓存')
					wx.reLaunch({
						url:'../Login/login'
					})
				},
				fail(err) {
					console.log('未清除缓存')
					
				}
			})
			}
		}
		
	}
</script>


<style lang="stylus" scoped>
	.ucenter-container
		background #F4F4F4
		.top
			background white
			.header
				background-image url(../../static/imgs/bj.webp)
				display  flex
				padding 53upx 0
				position relative
				.avatar
					width 200upx
					height 200upx
					overflow hidden
					border-radius 50%
					margin 0 30upx 0 40upx
					image
						width 100%
						height 100%
				.name
					display flex
					flex-direction column
					justify-content space-around
					padding 50upx 0
					font-size 30upx
					color white
				.prize
					width 46upx
					height 46upx
					position absolute
					top 75upx
					right 110upx
				.code
					width 66upx
					height 66upx
					overflow hidden
					position absolute
					top 60upx
					right 30upx
					image
						transform translateY(-83upx)
						height 1200upx
						width 100%
						
			.cardBag
				padding-left 30upx
				h2
					font-size 32upx
					border-bottom 1upx solid #F5F5F5
					padding 30upx 0
					color #333
				.card-list
					display flex
					font-size 27upx
					font-weight 500
					.card-item
						display flex
						flex-direction column
						align-items center
						width 25%
						padding 40upx 0
						span:nth-child(1)
							font-weight 600
							margin-bottom 20upx
		.model
			width 100%
			background white
			margin 20upx 0 40upx 0
			overflow hidden
			.model-item:nth-child(2)
				border 1upx solid #F4F4F4
				border-top none
			.model-item:nth-child(5)
				border 1upx solid #F4F4F4
				border-top none
			.model-item:nth-child(8)
				border 1upx solid #F4F4F4
				border-top none
			.model-item:nth-child(11)
				border 1upx solid #F4F4F4
				border-top none
			
			.model-item
				width 33%
				height 67upx
				float left
				display flex
				flex-direction column
				align-items center
				font-size 26upx
				border-bottom 1upx solid #F4F4F4
				padding 40upx 0
				div
					width 70upx
					height 70upx
					overflow hidden
					margin-bottom 10upx
					
		.bottom
			background white
			text-align center
			font-size 30upx
			color #333333
			padding 30upx 0
</style>

			
					
