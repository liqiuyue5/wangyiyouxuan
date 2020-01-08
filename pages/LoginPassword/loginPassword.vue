<template>
	<div>
		<image src="../../static/imgs/logo.png"></image>
		<div class='form'>
			<form action="">
					<div class="num">
						<input name="phone" type="text" value="" placeholder="请输入手机号"/>
						<div class="empty">x</div>
					</div>
					<div class="verification">
						<input name="password" type="text" placeholder="请输入密码" />
					</div>
					<div class="ques">
						<span>忘记密码？</span>
						<span @click="phoneLogin">短信快捷登陆</span>
					</div>
					<button type="primary">登录</button>
					<div class="other" @click="otherLogin">其他登陆方式></div>
				</form>
			
		</div>
	</div>
</template>

<script>
	export default{
		methods:{
			otherLogin(){
				wx.navigateTo({
					url:'../Login/login'
				})
			},
			phoneLogin(){
				wx.navigateTo({
					url:'../LoginPhone/loginphone'
				})
			}
		}
	}
</script>

<style lang="stylus" scoped>
	
	image
		width 267upx
		height 90upx
		margin-left 50%
		transform translateX(-50%)
		margin-top 150upx
	.form
		margin-left 50%
		transform translateX(-50%)
		width 670upx
		input
			border-bottom 1upx solid #F6F6F6
			width 100%
			font-size 30upx
			padding 20upx 0
		.num
			position relative
			.empty
				font-size 30upx
				background #D1D1D1
				border-radius 50%
				position absolute
				color white
				width 30upx
				height 30upx
				line-height 30upx
				text-align center
				padding-bottom 5upx
				top 37upx
				right 20upx
		.verification
			margin-top 20upx
			position relative
			.getcode
				position absolute
				font-size 30upx
				color #333333
				border 1upx solid #BEBEBE
				padding  5upx 10upx
				border-radius 5upx
				top 25upx
				right 20upx
		.ques
			display flex
			justify-content space-between
			padding 40upx 0
			font-size 32upx
			span:nth-child(1)
				color #8D8D8D
		button
			background #DD1A21
			font-size 30upx
			padding 10upx
		.doc
			font-size 30upx
			color #8D8D8D
			margin 20upx 0
			checkbox
				zoom 60%
		.other
			font-size 30upx
			color #333333
			text-align center
			margin 50upx 0
</style>
