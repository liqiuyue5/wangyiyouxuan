<template>
	<div>
		<image src="../../static/imgs/logo.png"></image>
		<div class='form'>
			<form action="">
					<div class="num">
						<input name="phone" type="text" placeholder="请输入手机号" v-model="phone"></input>
						<span style="color: #E44A50;font-size: 28upx;" v-show="!isRightPhone&&validateAll">手机号格式错误</span>
						<span style="color: #E44A50;font-size: 28upx;" v-show="!isRightPhone&&lili">手机号格式错误</span>
						<div class="empty" v-show='phone' @click="empty()">x</div>
					</div>
					<div class="verification">
						<input name="code" type="text" placeholder="请输入验证码" v-model="code"/>
						<span style="color: #E44A50;font-size: 28upx;" v-show="!isRightCode&&validateAll">请输入短信验证码</span>
						
						<button class="getcode" @click.prevent="sendcode()" v-show="isShow">获取验证码</button>
						<button class="getcode over" @click.prevent="sendcode()" disabled="flase" v-show="!isShow">{{time}}秒后重发</button>
					</div>
					<div class="ques">
						<span>遇到问题？</span>
						<span @click="passwordLogin">使用验证码登录</span>
					</div>
					<button type="primary" @click="login()">登录</button>
					<div class="docc">
						<label>
							<checkbox name="agree" :value="agree" v-model="agree" @click="isAgree"/><text>我同意《服务条款》和《网易隐私政策》</text><br/>
							<span style="color: #E44A50;font-size: 28upx;" v-show="!agree&&validateAll">您需要同意相关条例才能使用</span>
						</label>
					</div>
					<div class="other" @click="otherLogin">其他登陆方式></div>
				</form>
			
		</div>
	</div>
</template>

<script>
	import config from '../../utils/config.js'
	export default{
		data(){
			return{
				time:0,
				isShow:true,
				phone:'',
				code:'',
				agree:false,
				validateAll:false,
				lili:false
			}
		},
		computed:{
			isRightPhone () {
			        return /^1\d{10}$/.test(this.phone)
			},
			isRightCode() {
			        return /\d{5}$/.test(this.code)
			}
			
		},
		methods:{
			isAgree(){
				this.agree = !this.agree
			},
			empty(){
				this.phone = ''
			},
			otherLogin(){
				wx.navigateTo({
					url:'../Login/login'
				})
			},
			passwordLogin(){
				wx.navigateTo({
					url:'../LoginPassword/loginPassword'
				})
			},
			async sendcode(){
				const that = this
				if(this.isRightPhone){
					this.lili = false
					this.isShow=false
					this.time = 5
					await wx.request({
						url:`${config.host+'/sendcode'}`,
						data:{'phone':that.phone},
						method:"GET",
						success:function(res){
							console.log('请求成功')
						},
						fail:function(error){
							console.log(error.errMsg)
						}
					})
					const setinterId = setInterval(()=>{
						this.time= this.time-1
						if(this.time<=0){
							clearInterval(setinterId)
							this.isShow=!this.isShow
						}
					},1000)
				}else{
					this.lili = true
				}
			},
			async login(){
				this.validateAll = true
				const that = this
				if(this.isRightCode&&this.isRightPhone&&this.agree){
					wx.login({
						success:function(res){
							if(res.code){
								wx.request({
										url:`${config.host+'/login_sms'}`,
										data:{phone:that.phone,code:res.code},
										method:"POST",
										dataType: "json",
										header: {
										    'content-type': 'application/json' // 默认值
										},
										success:function(res){
											console.log(res.data)
											wx.navigateTo({
												url:'../Ucenter/ucenter'
											})
											wx.setStorage({
												'key':'isLogin',
												'data':true
											})
										},
										fail:function(error){
											console.log('请求失败')
											wx.showToast({
												title: '服务器崩溃啦！',
												icon: 'none',
												duration: 2000
											})
										}
									})
								
							}
						}
					})
									}
			},
			
			
		},
		watch:{
			
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
				z-index 99
		.verification
			margin-top 20upx
			position relative
			
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
		.docc
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
		.getcode
			position absolute
			font-size 26upx
			color #666
			top 20upx
			right 20upx
			background white
			height 60upx
			line-height 40upx
			z-index 99
			outline none
		.over 
			color #BEBEBE
</style>
