<script>
	export default {
		data(){
			return {
				cartFoods:[],
				id:0,
				checked:[]
			}
		},
		mounted(){
			uni.$on("getDetail",(id,checked)=>{
				console.log("11")
				this.id=id
				this.checked=checked
				console.log(this.checked)
			})
		},
		methods:{
			getId(index){
				this.index=index
			}
		},
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="stylus">
	/*每个页面公共css */
	@import url('./static/stylus/iconfont/iconfont.styl') 
	@import url('./static/stylus/iconfont/mxqiconfont.styl') 
	@import url('./static/stylus/iconfont/liqiuyueiconfont.styl')
	page 
		width 100%
		height 100% 
		// font-size 24upx
</style>
