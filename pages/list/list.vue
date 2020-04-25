<template>
	<view>
		
		<button @click="getRes">发送get请求</button>
		<button @click="postRes">发送post请求</button>
		<!-- <button @click="setStorge">存储数据</button>
		<button @click="getStorge">获取数据</button>
		<button @click="removeStorge">删除数据</button>
		<text >{{msg}}</text>
		<br> -->
		<view>
			<center>列表页</center>
		</view>
		<button @click="refresh">下拉刷新按钮</button>
		<!-- 列表页 -->
		<view class="box-item" v-for="(item) in list">
			{{item}}
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				list:[
					'java',
					'前端',
					'UI',
					'测试',
					'python',
					'php',
					'c++',
					'golang'
				],
				msg:''
			}
		},
		/* 下拉刷新出发事件 */
		onPullDownRefresh() {
			console.log('触发下拉刷新')
			/* 设置延时2秒 */
			setTimeout(()=>{
				this.list = ['运维','java','前端','UI','测试','python','php','大数据']
				uni.stopPullDownRefresh()
			},2000)
			
		},
		/* 页面到底触发事件 */
		onReachBottom() {
			console.log('页面到底了')
			/* es6扩展运算符 新增数据 */
			this.list = [...this.list,...['1-java','1-前端','1-UI','1-测试','1-python','1-php']]
		},
		methods:{
			/* 使用按钮的方式执行下拉刷新 */
			refresh(){
				console.log('下拉刷新按钮')
				uni.startPullDownRefresh()
			},
			getRes(){
				uni.request({
					url:"http://127.0.0.1:5000",
					method:'GET',
					success(res) {
						console.log(res)
					}
				})
			},
			postRes(){
				uni.request({
					url:"http://localhost:5000",
					method:'POST',
					success(res) {
						console.log(res)
					}
				})
			},
			setStorge(){
				uni.setStorage({
					key:'id',
					data:80,
					success() {
						console.log('存储成功')
					}
				})
			},
			getStorge(){
				uni.getStorage({
					key:'id',
					/* 如果双向绑定值，只能这样写 */
					success: (data) => {
						console.log('获取成功',data)
						this.msg = data.data
					}
				})
			},
			removeStorge(){
				uni.removeStorage({
					key:'id',
					success() {
						console.log('删除成功')
					}
				})
			}
		}
	}
	
</script>

<style>
	.box-item{
		height: 100px;
		line-height: 100px;
	}
	
</style>
