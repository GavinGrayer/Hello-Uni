<template>
	<view>
		<view>
			页面跳转
		</view>
		<!-- 跳转普通页面 -->
		<br>
		<h2>-----声明式页面跳转-----</h2>
		<navigator url="../detail/detail?id=80&age=22">
			<button type="primary">跳转至详情页1</button>
		</navigator>
		<!-- navigateTo:fail can not navigateTo a tabbar page
		 跳转tab页面必须设置open-type="switchTab"
		 -->
		<navigator url="../message/message" open-type="switchTab">
			<button type="primary">跳转至信息页</button>
		</navigator>
		<!-- open-type="redirect"不带返回按键返回先前页面，会关闭当前页面 -->
		<navigator url="../detail/detail" open-type="redirect">
			<button type="primary">跳转至详情页2</button>
		</navigator>
	
		
		<!-- 编程式导航跳转 -->
		<br>
		<view>
			<h2>-----编程式页面跳转------</h2>
		</view>
		<button @click="goDetail" type="primary">跳转至详情页1</button>
		<button @click="goMsg" type="primary">跳转信息页</button>
		<button @click="goDeatilTwo" type="primary">跳转详情页并关闭当前页面</button>
	</view>
</template>

<script>
	export default{
		onUnload() {
			console.log('卸载了')
		},
		methods:{
			goDetail(){
				uni.navigateTo({
					url:'../detail/detail?id=80&age=22'
				})
			},
			goDeatilTwo(){
				console.log('1111')
				uni.redirectTo({
					url:'../detail/detail'
				})
			},
			goMsg(){
				/* 跳转tab页面，会卸载非tab页面 */
				uni.switchTab({
					url:'../message/message'
				})
			}
		}
	}
</script>

<style>
</style>
