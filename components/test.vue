<template>
	<view id="myView">
		这是test组件{{msg}}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				msg:'123',
				intId : null
			};
		},
		beforeCreate() { //在实例初始化之后，data数据配置之前被调用
			console.log('beforeCreate::',this.msg)
		},
		created() { //在实例创建完成后被立即调用
			console.log('created::',this.msg)
			this.intId = setInterval(()=>{
				console.log('执行定时器')
			},1000)
		},
		beforeMount() {
			console.log('beforeMount::',document.getElementById('myView'))
		},
		mounted() {
			console.log('mounted::',document.getElementById('myView'))
		},
		destroyed() {
			console.log('destroyed::组件销毁')
			//定时器销毁
			clearInterval(this.intId)
		}
		
	}
</script>

<style>

</style>
