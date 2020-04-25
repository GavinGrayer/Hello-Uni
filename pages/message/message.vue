<template>
	<view>
		hello	

		<view>
			<!--selectable：可选文字
			  space 空格
			  style 样式-->
<!-- 			<text 
			selectable="true"
			 space="emsp"
			  style="font-size: 30px;">
			  哈&amp;哈哈
			  </text> -->
			  
			  <button type="primary" @click="chooseImg">上传图片</button>
			  <image v-for="item in imgArr" :src="item" @click="prevImg(item)"></image>
				<!-- #ifdef H5 -->
				<view>
				  h5页面会显示
				</view>
				<!-- #endif -->
				<!-- #ifdef MP-WEIXIN -->
				<view>
				  微信小程序会显示
				</view>
				<!-- #endif -->
				<!-- #ifdef APP-PLUS -->
				<view>
				  app会显示
				</view>
				<!-- #endif -->
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				imgArr:[]
			}
		},
		methods:{
			chooseImg(){
				console.log('上传图片')
				uni.chooseImage({
					count:5,
					success:res=> {
						console.log(res)
						this.imgArr = res.tempFilePaths
						console.log('imgArr::',imgArr)
					}
				})
			},
			/* 预览图片 */
			prevImg(current){
				console.log(current)
				uni.previewImage({
					current:current,
					urls:this.imgArr,
					loop:true,
					indicator:'number'
				})
			}
		}
	}
</script>


<style>
	/* h5中的样式 */
	/* #ifdef H5 */
	view{
		color: hotpink;
	}
	/* #endif */
	/* 微信小程序中的样式 */
	/* #ifdef MP-WEIXIN */
	view{
		color: #0000FF;
	}
	/* #endif */
</style>

