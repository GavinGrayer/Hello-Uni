<template>
	<!-- view 类似 div 
	class 设置样式
	hover-class 按住样式
	-->

	
	<view class="box2" hover-class="box2-active">
		<view
		class="box" 
		hover-class="box-active" 
		hover-start-time="0" 
		hover-stay-time="0"
		hover-stop-propagation="true">联系我们
		
		</view>
		<!-- 
		 size: 大小
		 type：按钮类型
		 plain： 镂空
		 disabled: 是否禁用
		 -->
		<button size="mini" type="primary" plain disabled>按钮</button>
		<button loading="" class="icon-guanyuwomen"></button>
		<!-- src: 可以线上可以线下 
		aspectFit：保证长边正常显示，进行长宽缩放
		aspectFill： 保证短边正常显示，进行长宽缩放
		-->
		<image src="http://destiny001.gitee.io/image/cxk.gif"></image>
		<image src="http://destiny001.gitee.io/image/cxk.gif" mode="aspectFit"></image>
		<image src="http://destiny001.gitee.io/image/cxk.gif" mode="aspectFill"></image>
	</view>
</template>

<script>
</script>

<style>
	.box{
		width: 100px;
		height: 100px;
		background-color: #007AFF;
	}
	.box-active{
		background: red;
	}
	.box2{
		width: 200px;
		height: 200px;
		background-color: #4CD964;
	}
	.box2-active{
		background: #FF0000;
	}
</style>
