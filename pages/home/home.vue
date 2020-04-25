<template>
	<view>
		数据绑定{{msg}}
		<view>
			{{1+'你好'+'世界'}}<br>
			{{1+1}}<br>
			<!-- 三目运算符 -->
			{{flag == 0 ? 'true' : 'false'}}
		</view>
		<!-- :src   获取data中定义的数据 -->
		 <image :src="imgUrl"></image>
		 <!-- for遍历-->
		 <view v-for="(item,index) in arr" :key="index">
			 序号：{{item.id}}，名字：{{item.name}}，年龄: {{item.age}}
		 </view>
		 <!-- 点击事件 参数 和 $event传递事件对象-->
		 <button type="primary" v-on:click="clickHandle(20,$event)">按钮</button>
		 <!--v-on:click  和   @click 等价-->
		 <button type="primary" @click="clickHandle(20,$event)">按钮2</button>
	</view>
</template> 

<script>
	export default{
		data(){
			return{
				msg:'hello world',
				flag:'0',
				imgUrl: 'http://destiny001.gitee.io/image/monkey_02.jpg',
				arr:[
					{name:'张三',age: 20,id: 1},
					{name:'李四',age: 20,id: 2},
					{name:'王五',age: 20,id: 3}
				]
			}
		},
		methods:{
			clickHandle(param,e){
				console.log("click::",param,e)
			}
		}
	
	}
</script>

<style>
</style>
