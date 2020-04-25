<template>
	<view>
		<view>
			<!-- 插值表达式 -->
			样式的学习{{msg}}
		</view>
		<view class="box1">
			测试文字
			<text>123</text>
		</view>
		<view class="iconfont icon-tupian">123</view>
	</view>
</template>

<script>
	export default{
		data(){
			return {
				msg: 'hello'
			}
		}
	}
</script>

<style>
	/* 外联样式表 */
	@import url("./a.css");
	.box1{
		width: 375rpx;
		height: 375rpx;
		/* background: #33b5e5; */
		background: $global-color;
		font-size: 30rpx;
		color: #fff;
		text{
			color: pink;
		}
	}
</style>
