<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title" >{{title}}</text>
			<br>
		</view>
			<button type="primary" @click="checkFlag">销毁组件</button>
		<!-- 加入components组件 -->
		<test v-if="flag"></test>
		
		<view>
		    <uni-calendar 
		    :insert="true"
		    :lunar="true" 
		    :start-date="'2019-3-2'"
		    :end-date="'2019-5-20'"
		    @change="change"
		     ></uni-calendar>
		</view>
	</view>
</template>

<script>
	import test from '../../components/test.vue'
	
	import uniCalendar from '@/components/uni-calendar/uni-calendar.vue'
	
	export default {
		data() {
			return {
				title: 'Hello',
				flag:true
			}
		},
		/* 当前面跳转过来传参会存到 options 中*/
		onLoad(options) {
			console.log('页面生命周期——页面加载',options)
		},
		onShow() {
			console.log('页面生命周期——页面显示了')
		},
		onReady(){
			console.log('页面生命周期——页面初次渲染完成')
		},
		onHide() {
			console.log('页面生命周期——页面隐藏了')
		},
		methods: {
			checkFlag(){
				console.log('手动销毁')
				this.flag = false
			},
			change(e) {
				console.log('日历组件::',e);
			}
		},
		components:{
			test:test,
			uniCalendar
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
