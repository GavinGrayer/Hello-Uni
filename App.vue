<script>
	/* 生命周期函数 */
	export default {
		onLaunch: function() {
			console.log('App Launch  初始化完成时触发')
		},
		onShow: function() {
			console.log('App Show 显示应用')
		},
		/* 类似  手机 按home键 */
		onHide: function() {
			console.log('App Hide 隐藏应用')
		},
		onError:function(err){
			console.log('App Error 触发异常',err)
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import url("./static/fonts/iconfont.css");
	/* .box1{
		background: #33b5e5;
	} */
</style>
