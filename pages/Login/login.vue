<template>
	<div class='login'>
		<image src="../../static/imgs/logo.png" mode=""></image>
		<div class="phone" @click='gophone'>手机号快捷登陆</div>
		<div class="email" @click='goemail'>邮箱账号登录</div>
		<div class="other">
			<button class="weixin" open-type="getUserInfo" @getuserinfo="bindGetUserInfo">微信</button>
			<div class='line'></div><button class="qq">QQ</button>
			<div class='line'></div><button class="weibo">微博</button>
		</div>
	</div>
</template>

<script>
	export default{
		methods:{
			gophone(){
				wx.navigateTo({
					url:'../LoginPhone/loginphone'
				})
			},
			goemail(){
				wx.navigateTo({
					url:'../LoginEmail/loginemail'
				})
			},
			bindGetUserInfo(res){
				if(res.mp.detail.userInfo){
					console.log(res.mp.detail.userInfo)
					wx.showToast({
						title:'登录成功',
						// duration: 5000,  // 貌似不生效
						success: () => {
							// reLaunch解决跳转能tabBar传参的问题
							wx.setStorage({
								'key':'isLogin',
								'data':true
							})
							wx.reLaunch({
								url: '/pages/Ucenter/ucenter'
							})
						}
					})
					
				}else {

					wx.showToast({
						title: '授权失败，请重新授权'
					})
				}	
			}
			
		}
		
	}
</script>

<style lang="stylus" scoped>
	
		.login
			width 100%
			height 100vh
			background #F2F5F4
			image
				width 267upx
				height 90upx
				margin-left 50%
				transform translateX(-50%)
				margin-top 150upx
			.phone
				background #DD1A21
				color white
				text-align center
				padding  25upx 30upx
				width 600upx
				margin-left 50%
				transform translateX(-50%)
				font-size 30upx
				margin-top 250upx
			.email
				text-align center
				padding  25upx 30upx
				width 600upx
				margin-left 50%
				transform translateX(-50%)
				font-size 30upx
				border 1upx solid #DD1A21
				color #DD1A21
				margin-top 30upx
			.other
				display flex
				padding 0 140upx
				margin 400upx 0 0 0
				div
					width 4upx
					height 40upx
					background #BFC1C0
					margin 20upx
				button
					width 200upx
					text-align center
					padding 0
					font-size 30upx
					color #7F7F7F
					background #F2F5F4
				button::after
					border none
				
</style>
