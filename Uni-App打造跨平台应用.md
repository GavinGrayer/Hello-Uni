
# 介绍

`uni-app` 是一个使用 [Vue.js](https://vuejs.org/) 开发所有前端应用的框架，开发者编写一套代码，可发布到iOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉）等多个平台。学会uni-app之后，即可开发出iOS、Android、H5、以及各种小程序的应用，不需要再去学习开发其他应用的框架。



# 安装

安装编辑器HbuilderX  [下载地址](https://www.dcloud.io/hbuilderx.html)

HBuilderX是通用的前端开发工具，但为`uni-app`做了特别强化。

下载App开发版，可开箱即用

安装微信开发者工具 [下载地址](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)



# Demo

## 上手

### 创建默认Demo

1、点击HbuilderX菜单栏文件>项目>新建

2、选择uni-app,填写项目名称，项目创建的目录

![image-20200423150113665](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423150113665.png)

### 运行

在菜单栏中点击运行，运行到浏览器，选择浏览器即可运行

![image-20200423150341913](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423150341913.png)

也可以跳转到微信开发者工具，或者App真机测试（安装ADB即可）



## 项目结构

1、`pages.json` 文件用来对 uni-app 进行全局配置，决定页面文件的路径、窗口样式、原生的导航栏、底部的原生tabbar 等

2、`manifest.json` 文件是应用的配置文件，用于指定应用的名称、图标、权限等。

3、`App.vue`是我们的跟组件，所有页面都是在`App.vue`下进行切换的，是页面入口文件，可以调用应用的生命周期函数。

4、`main.js`是我们的项目入口文件，主要作用是初始化`vue`实例并使用需要的插件。

5、`uni.scss`文件的用途是为了方便整体控制应用的风格。比如按钮颜色、边框风格，`uni.scss`文件里预置了一批scss变量预置。

6、```unpackage``` 就是打包目录，在这里有各个平台的打包文件

7、```pages``` 所有的页面存放目录

8、```static``` 静态资源目录，例如图片等

9、```components``` 组件存放目录



# 全局配置和页面配置

## 通过globalStyle进行全局配置

> 位于项目根目录pages.json中
>
> ![image-20200423151010021](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423151010021.png)



用于设置应用的状态栏、导航条、标题、窗口背景色等。[详细文档](https://uniapp.dcloud.io/collocation/pages?id=globalstyle)

| 属性                         | 类型     | 默认值  | 描述                                                         |
| ---------------------------- | -------- | ------- | ------------------------------------------------------------ |
| navigationBarBackgroundColor | HexColor | #F7F7F7 | 导航栏背景颜色（同状态栏背景色）                             |
| navigationBarTextStyle       | String   | white   | 导航栏标题颜色及状态栏前景颜色，仅支持 black/white           |
| navigationBarTitleText       | String   |         | 导航栏标题文字内容                                           |
| backgroundColor              | HexColor | #ffffff | 窗口的背景色                                                 |
| backgroundTextStyle          | String   | dark    | 下拉 loading 的样式，仅支持 dark / light                     |
| enablePullDownRefresh        | Boolean  | false   | 是否开启下拉刷新，详见[页面生命周期](https://uniapp.dcloud.io/use?id=%e9%a1%b5%e9%9d%a2%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f)。 |
| onReachBottomDistance        | Number   | 50      | 页面上拉触底事件触发时距页面底部距离，单位只支持px，详见[页面生命周期](https://uniapp.dcloud.io/use?id=%e9%a1%b5%e9%9d%a2%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f) |

## 创建新的message页面

右键pages新建message目录，在message目录下右键新建.vue文件,并选择基本模板

```html
<template>
	<view>
		这是信息页面
	</view>
</template>

<script>
</script>

<style>
</style>
```

## 通过pages来配置页面

| 属性  | 类型   | 默认值 | 描述                                                         |
| ----- | ------ | ------ | ------------------------------------------------------------ |
| path  | String |        | 配置页面路径                                                 |
| style | Object |        | 配置页面窗口表现，配置项参考 [pageStyle](https://uniapp.dcloud.io/collocation/pages?id=style) |

<span style="color:red">**pages数组数组中第一项表示应用启动页**</span>

```json
"pages": [
		{
			"path":"pages/message/message"//默认加载这个页面
		},
		{
			"path": "pages/index/index",
			"style": {
				"navigationBarTitleText": "uni-app"
			}
		}
	]
```

通过style修改页面的标题和导航栏背景色，并且设置h5下拉刷新的特有样式

```js
"pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
		{
			"path":"pages/message/message",
			"style":{
				"navigationBarTitleText":"信息页",
				"navigationBarBackgroundColor":"#F0AD4E",
				"h5":{
					"pullToRefresh":{
						"color":"#7D26CD"
					}
				}
			}
		}
	]
```
效果如下：

![page配置页面](http://img.mxranger.cn/Uni-App打造跨平台应用/page配置页面.gif)

## 配置tabbar

如果应用是一个多 tab 应用，可以通过 tabBar 配置项指定 tab 栏的表现，以及 tab 切换时显示的对应页（类似Android中的fragment）。

**Tips**

- 当设置 position 为 top 时，将不会显示 icon
- tabBar 中的 list 是一个数组，只能配置最少2个、最多5个 tab，tab 按数组的顺序排序。

**属性说明：**

| 属性            | 类型     | 必填 | 默认值 | 描述                                                 | 平台差异说明              |
| --------------- | -------- | ---- | ------ | ---------------------------------------------------- | ------------------------- |
| color           | HexColor | 是   |        | tab 上的文字默认颜色                                 |                           |
| selectedColor   | HexColor | 是   |        | tab 上的文字选中时的颜色                             |                           |
| backgroundColor | HexColor | 是   |        | tab 的背景色                                         |                           |
| borderStyle     | String   | 否   | black  | tabbar 上边框的颜色，仅支持 black/white              | App 2.3.4+ 支持其他颜色值 |
| list            | Array    | 是   |        | tab 的列表，详见 list 属性说明，最少2个、最多5个 tab |                           |
| position        | String   | 否   | bottom | 可选值 bottom、top                                   | top 值仅微信小程序支持    |

其中 list 接收一个数组，数组中的每个项都是一个对象，其属性值如下：

| 属性             | 类型   | 必填 | 说明                                                         |
| ---------------- | ------ | ---- | ------------------------------------------------------------ |
| pagePath         | String | 是   | 页面路径，必须在 pages 中先定义                              |
| text             | String | 是   | tab 上按钮文字，在 5+APP 和 H5 平台为非必填。例如中间可放一个没有文字的+号图标 |
| iconPath         | String | 否   | 图片路径，icon 大小限制为40kb，建议尺寸为 81px * 81px，当 postion 为 top 时，此参数无效，不支持网络图片，不支持字体图标 |
| selectedIconPath | String | 否   | 选中时的图片路径，icon 大小限制为40kb，建议尺寸为 81px * 81px ，当 postion 为 top 时，此参数无效 |

案例代码：

```js
"tabBar": {
		"list": [
			{
				"text": "首页",
				"pagePath":"pages/index/index",
				"iconPath":"static/tabs/home.png",
				"selectedIconPath":"static/tabs/home-active.png"
			},
			{
				"text": "信息",
				"pagePath":"pages/message/message",
				"iconPath":"static/tabs/message.png",
				"selectedIconPath":"static/tabs/message-active.png"
			},
			{
				"text": "我们",
				"pagePath":"pages/contact/contact",
				"iconPath":"static/tabs/contact.png",
				"selectedIconPath":"static/tabs/contact-active.png"
			}
		]
	}
```

效果如下：

![配置tabbar](http://img.mxranger.cn/Uni-App打造跨平台应用/配置tabbar.gif)



## condition启动模式配置

启动模式配置，仅开发期间生效，用于**模拟直达页面**的场景，如：小程序转发后，用户点击所打开的页面。

**属性说明：**

| 属性    | 类型   | 是否必填 | 描述                             |
| ------- | ------ | -------- | -------------------------------- |
| current | Number | 是       | 当前激活的模式，list节点的索引值 |
| list    | Array  | 是       | 启动模式列表                     |

**list说明：**

| 属性  | 类型   | 是否必填 | 描述                                                         |
| ----- | ------ | -------- | ------------------------------------------------------------ |
| name  | String | 是       | 启动模式名称                                                 |
| path  | String | 是       | 启动页面路径                                                 |
| query | String | 否       | 启动参数，可在页面的 [onLoad](https://uniapp.dcloud.io/use?id=%e9%a1%b5%e9%9d%a2%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f) 函数里获得 |

# Uni-App的相关组件

uni-app提供了丰富的基础组件给开发者，开发者可以像搭积木一样，组合各种组件拼接称自己的应用

uni-app中的组件，就像 `HTML` 中的 `div` 、`p`、`span` 等标签的作用一样，用于搭建页面的基础结构

## text

|    属性    |  类型   | 默认值 | 必填 |                      说明                      |
| :--------: | :-----: | :----: | :--: | :--------------------------------------------: |
| selectable | boolean | false  |  否  |                  文本是否可选                  |
|   space    | string  |   .    |  否  | 显示连续空格，可选参数：`ensp`、`emsp`、`nbsp` |
|   decode   | boolean | false  |  否  |                    是否解码                    |

- `text` 组件相当于行内标签、在同一行显示
- 除了文本节点以外的其他节点都无法长按选中





## view

> View 视图容器， 类似于 HTML 中的 div



### 组件属性

![image-20200423155350946](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423155350946.png)





### 代码案例

```vue
<view class="box2" hover-class="box2-active">
    <view
          class="box" 
          hover-class="box-active" 
          hover-start-time="0" 
          hover-stay-time="0"
          hover-stop-propagation="true">联系我们

    </view>
</view>

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
```

效果如下：

![view视图点击](http://img.mxranger.cn/Uni-App打造跨平台应用/view视图点击.gif)





## button

### 组件的属性

|  属性名  |  类型   | 默认值  |           说明           |
| :------: | :-----: | :-----: | :----------------------: |
|   size   | String  | default |        按钮的大小        |
|   type   | String  | default |      按钮的样式类型      |
|  plain   | Boolean |  false  | 按钮是否镂空，背景色透明 |
| disabled | Boolean |  false  |         是否按钮         |
| loading  | Boolean |  false  | 名称是否带 loading t图标 |

- `button` 组件默认独占一行，设置 `size` 为 `mini` 时可以在一行显示多个

### 案例代码

```html
<button size="mini" type="primary" plain disabled>按钮</button>
```

![image-20200423160646723](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423160646723.png)



## image

> [image](https://uniapp.dcloud.io/component/image?id=image)

### 属性

| 属性名 | 类型   | 默认值        | 说明                 | 平台差异说明 |
| ------ | ------ | ------------- | -------------------- | ------------ |
| src    | String |               | 图片资源地址         |              |
| mode   | String | 'scaleToFill' | 图片裁剪、缩放的模式 |              |

**Tips**

- `<image>` 组件默认宽度 300px、高度 225px；
- `src` 仅支持相对路径、绝对路径，支持 base64 码；
- 页面结构复杂，css样式太多的情况，使用 image 可能导致样式生效较慢，出现 “闪一下” 的情况，此时设置 `image{will-change: transform}` ,可优化此问题。



### 案例

```vue
<!-- src: 可以线上可以线下 
		aspectFit：保证长边正常显示，进行长宽缩放
		aspectFill： 保证短边正常显示，进行长宽缩放
		-->
		<image src="http://destiny001.gitee.io/image/cxk.gif"></image>
		<image src="http://destiny001.gitee.io/image/cxk.gif" mode="aspectFit"></image>
		<image src="http://destiny001.gitee.io/image/cxk.gif" mode="aspectFill"></image>
```



## 外部样式引入

1. 去iconfont下载第三方UI相关样式

2. 在当前项目根目录，创建static文件夹，将相关文件放入

![image-20200423161911894](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423161911894.png)

3. 在`iconfont.css`文件中，字体文件的引用路径推荐使用以 ~@ 开头的绝对路径

```css
 @font-face {
     font-family: test1-icon;
     src: url('~@/static/iconfont.ttf');
 }
```

![image-20200423162032457](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423162032457.png)



4. 在App.vue文件中引入公共css作为全局属性，保证每个组件都能使用

```vue
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

```



**注意：**

+ rpx 即响应式px，一种根据屏幕宽度自适应的动态单位。以750宽的屏幕为基准，750rpx恰好为屏幕宽度。屏幕变宽，rpx 实际显示效果会等比放大。

+ 使用`@import`语句可以导入外联样式表，`@import`后跟需要导入的外联样式表的相对路径，用`;`表示语句结束

+ 支持基本常用的选择器class、id、element等

+ 在 `uni-app` 中不能使用 `*` 选择器。

+ `page` 相当于 `body` 节点

+ 定义在 App.vue 中的样式为全局样式，作用于每一个页面。在 pages 目录下 的 vue 文件中定义的样式为局部样式，只作用在对应的页面，并会覆盖 App.vue 中相同的选择器。

+ `uni-app` 支持使用字体图标，使用方式与普通 `web` 项目相同，需要注意以下几点：
- 字体文件小于 40kb，`uni-app` 会自动将其转化为 base64 格式；
  
- 字体文件大于等于 40kb， 需开发者自己转换，否则使用将不生效；
  
- 字体文件的引用路径推荐使用以 ~@ 开头的绝对路径。





## css样式引入

### 创建a.css文件

```css
view{
	color: green;
}
```

### vue文件

```vue
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

```

效果如下：

![image-20200424095258593](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200424095258593.png)







# 数据绑定

在页面中需要定义数据，和我们之前的vue一摸一样，直接在data中定义数据即可

```js
export default {
  data () {
    return {
      msg: 'hello-uni'
    }
  }
}
```

## 插值表达式的使用

+ 利用插值表达式渲染基本数据

  ```html
  <view>{{msg}}</view>
  ```

+ 在插值表达式中使用三元运算

  ```html
  <view>{{ flag ? '我是真的':'我是假的' }}</view>
  ```

+ 基本运算

  ```html
  <view>{{1+1}}</view>
  ```

## v-bind动态绑定属性

在data中定义了一张图片，我们希望把这张图片渲染到页面上

```js
export default {
  data () {
    return {
      img: 'http://destiny001.gitee.io/image/monkey_02.jpg'
    }
  }
}
```

利用v-bind进行渲染

```html
<image v-bind:src="img"></image>
```

还可以缩写成:

```html
<image :src="img"></image>
```

## v-for的使用

data中定以一个数组，最终将数组渲染到页面上

```js
data () {
  return {
      arr:[
          {name:'张三',age: 20,id: 1},
          {name:'李四',age: 20,id: 2},
          {name:'王五',age: 20,id: 3}
      ]
  }
}
```

利用v-for进行循环

```js
<!-- for遍历-->
    <view v-for="(item,index) in arr" :key="index">
        序号：{{item.id}}，名字：{{item.name}}，年龄: {{item.age}}
</view>
```

![image-20200423163248102](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200423163248102.png)



# 事件绑定和传参

- 如果给事件函数传递参数了，则对应的事件函数形参接收的则是传递过来的数据

  ```vue
  // template
  <button type="primary" @click="clickHandle(20)">按钮2</button>
  // script
  methods: {
    clickHandle (num) {
      console.log(num)
    }
  }
  ```

- 如果获取事件对象也想传递参数

  ```vue
  // template
  <!--v-on:click  和   @click 等价-->
  <button type="primary" @click="clickHandle(20,$event)">按钮2</button>
  // script
  methods: {
    clickHandle (num,e) {
      console.log(num,e)
    }
  }
  ```



效果如下：

![按钮事件绑定](http://img.mxranger.cn/Uni-App打造跨平台应用/按钮事件绑定.gif)



# 生命周期

## 应用的生命周期

生命周期的概念：一个对象从创建、运行、销毁的整个过程被成为生命周期。

生命周期函数：在生命周期中每个阶段会伴随着每一个函数的触发，这些函数被称为生命周期函数

`uni-app` 支持如下应用生命周期函数：

| 函数名   | 说明                                           |
| -------- | ---------------------------------------------- |
| onLaunch | 当`uni-app` 初始化完成时触发（全局只触发一次） |
| onShow   | 当 `uni-app` 启动，或从后台进入前台显示        |
| onHide   | 当 `uni-app` 从前台进入后台                    |
| onError  | 当 `uni-app` 报错时触发                        |


### 案例

App.vue的生命周期

```vue
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
```

效果如下：

![生命周期](http://img.mxranger.cn/Uni-App打造跨平台应用/生命周期.gif)





## 页面的生命周期

`uni-app` 支持如下页面生命周期函数：

| 函数名   | 说明                                                         | 平台差异说明 | 最低版本 |
| -------- | ------------------------------------------------------------ | ------------ | -------- |
| onLoad   | 监听页面加载，其参数为上个页面传递的数据，参数类型为Object（用于页面传参），参考[示例](https://uniapp.dcloud.io/api/router?id=navigateto) |              |          |
| onShow   | 监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面 |              |          |
| onReady  | 监听页面初次渲染完成。                                       |              |          |
| onHide   | 监听页面隐藏                                                 |              |          |
| onUnload | 监听页面卸载                                                 |              |          |



### 案例

```vue
<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title" >{{title}}</text>
			<br>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
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
```



# 下拉刷新

## 开启下拉刷新

在uni-app中有两种方式开启下拉刷新

+ 需要在 `pages.json` 里，找到的当前页面的pages节点，并在 `style` 选项中开启 `enablePullDownRefresh`
+ 通过调用uni.startPullDownRefresh方法来开启下拉刷新



## 关闭下拉刷新

| 下拉API事件 | 解释 |
| ------------------------- | ---- |
| uni.stopPullDownRefresh() |      停止当前页面下拉刷新|



## 监听下拉刷新

### 使用自带方式

```vue
<template>
	<view>
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
				list:['java','前端','UI','测试','python','php','c++','golang'],
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
		}
	}
	
</script>
```

效果如下：

![下拉刷新](http://img.mxranger.cn/Uni-App打造跨平台应用/下拉刷新.gif)



### 自定义刷新按钮

```vue
<template>
	<view>
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
				list:['java','前端','UI','测试','python','php','c++','golang'],
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
        methods:{
			/* 使用按钮的方式执行下拉刷新 */
			refresh(){
				console.log('下拉刷新按钮')
				uni.startPullDownRefresh()
            },
        }
	}
	
</script>
```

效果如下：

![下拉刷新按钮](http://img.mxranger.cn/Uni-App打造跨平台应用/下拉刷新按钮.gif)



# 页面底部上拉加载

通过在pages.json文件中找到当前页面的pages节点下style中配置onReachBottomDistance可以设置距离底部开启加载的距离，默认为50px

通过onReachBottom监听到触底的行为

```vue
<template>
	<view>
		<button type="primary" @click="startPull">开启下拉刷新</button>
		杭州学科
		<view v-for="(item,index) in arr" :key="index">
			{{item}}
		</view>
	</view>
</template>
<script>
	export default {
		data () {
			return {
				arr: ['前端','java','ui','大数据','前端','java','ui','大数据']
			}
		},
		onReachBottom () {
			console.log('触底了')
            this.list = [...this.list,...['1-java','1-前端','1-UI','1-测试','1-python','1-php']]
		}
	}
</script>

<style>
	view{
		height: 100px;
		line-height: 100px;
	}
</style>
```

效果如下：

![页面底部上拉加载](http://img.mxranger.cn/Uni-App打造跨平台应用/页面底部上拉加载.gif)



# 网络请求

在uni中可以调用uni.request方法进行请求网络请求

需要注意的是：在小程序中网络相关的 API 在使用前需要配置域名白名单。

## 发送get请求

```js
<template>
	<view>
		<button @click="sendGet">发送请求</button>
	</view>
</template>
<script>
	export default {
		methods: {
			sendGet () {
				uni.request({
					url:"http://127.0.0.1:5000",
					method:'GET',
					success(res) {
						console.log(res)
					}
				})
			}
		}
	}
</script>
```

## 发送post请求

和上面类似

```vue
<template>
	<view>
		<button @click="sendPost">发送请求</button>
	</view>
</template>
<script>
	export default {
		methods: {
			sendPost () {
				uni.request({
					url:"http://127.0.0.1:5000",
                    data:{
                        //参数  比如
                        data: data
                    },
                    header:{
                        // .......
                    }
					method:'POST',
					success(res) {
						console.log(res)
					}
				})
			}
		}
	}
</script>
```



# 数据缓存

## **uni.setStorage**

[官方文档](https://uniapp.dcloud.io/api/storage/storage?id=setstorage)

将数据存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个异步接口。

代码演示

```js
<template>
	<view>
		<button type="primary" @click="setStor">存储数据</button>
	</view>
</template>

<script>
	export default {
		methods: {
			setStor () {
				uni.setStorage({
				 	key: 'id',
				 	data: 100,
				 	success () {
				 		console.log('存储成功')
				 	}
				 })
			}
		}
	}
</script>

<style>
</style>
```

## uni.setStorageSync

将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个同步接口。

代码演示

```js
<template>
	<view>
		<button type="primary" @click="setStor">存储数据</button>
	</view>
</template>

<script>
	export default {
		methods: {
			setStor () {
				uni.setStorageSync('id',100)
			}
		}
	}
</script>

<style>
</style>
```

## uni.getStorage

从本地缓存中异步获取指定 key 对应的内容。

代码演示

```html
<template>
	<view>
		<button type="primary" @click="getStorage">获取数据</button>
	</view>
</template>
<script>
	export default {
		data () {
			return {
				id: ''
			}
		},
		methods: {
			getStorage () {
				uni.getStorage({
					key: 'id',
					success:  res=>{
						this.id = res.data
					}
				})
			}
		}
	}
</script>
```

## uni.getStorageSync

从本地缓存中同步获取指定 key 对应的内容。

代码演示

```html
<template>
	<view>
		<button type="primary" @click="getStorage">获取数据</button>
	</view>
</template>
<script>
	export default {
		methods: {
			getStorage () {
				const id = uni.getStorageSync('id')
				console.log(id)
			}
		}
	}
</script>
```

## uni.removeStorage

从本地缓存中异步移除指定 key。

代码演示

```html
<template>
	<view>
		<button type="primary" @click="removeStorage">删除数据</button>
	</view>
</template>
<script>
	export default {
		methods: {
			removeStorage () {
				uni.removeStorage({
					key: 'id',
					success: function () {
						console.log('删除成功')
					}
				})
			}
		}
	}
</script>
```

## uni.removeStorageSync

从本地缓存中同步移除指定 key。

代码演示

```html
<template>
	<view>
		<button type="primary" @click="removeStorage">删除数据</button>
	</view>
</template>
<script>
	export default {
		methods: {
			removeStorage () {
				uni.removeStorageSync('id')
			}
		}
	}
</script>
```



# 上传预览图片

uni.chooseImage方法从本地相册选择图片或使用相机拍照。

案例代码

```html
<template>
	<view>
		 <button type="primary" @click="chooseImg">上传图片</button>
		 <image v-for="item in imgArr" :src="item" @click="prevImg(item)"></image>
	</view>
</template>

<script>
	export default {
		data () {
			return {
				imgArr: []
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
```

效果如下：

![图片上传预览](http://img.mxranger.cn/Uni-App打造跨平台应用/图片上传预览.gif)



# 条件注释实现跨段兼容

条件编译是用特殊的注释作为标记，在编译时根据这些特殊的注释，将注释里面的代码编译到不同平台。

**写法：**以` #ifdef `加平台标识 开头，以 #endif 结尾。

平台标识

| 值         | 平台                                                   | 参考文档                                                     |
| ---------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| APP-PLUS   | 5+App                                                  | [HTML5+ 规范](http://www.html5plus.org/doc/)                 |
| H5         | H5                                                     |                                                              |
| MP-WEIXIN  | 微信小程序                                             | [微信小程序](https://developers.weixin.qq.com/miniprogram/dev/api/) |
| MP-ALIPAY  | 支付宝小程序                                           | [支付宝小程序](https://docs.alipay.com/mini/developer/getting-started) |
| MP-BAIDU   | 百度小程序                                             | [百度小程序](https://smartprogram.baidu.com/docs/develop/tutorial/codedir/) |
| MP-TOUTIAO | 头条小程序                                             | [头条小程序](https://developer.toutiao.com/dev/cn/mini-app/develop/framework/basic-reference/introduction) |
| MP-QQ      | QQ小程序                                               | （目前仅cli版支持）                                          |
| MP         | 微信小程序/支付宝小程序/百度小程序/头条小程序/QQ小程序 |                                                              |

## 组件的条件注释

代码演示

```html
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
```

## api的条件注释

代码演示

```js
onLoad () {
  //#ifdef MP-WEIXIN
  console.log('微信小程序')
  //#endif
  //#ifdef H5
  console.log('h5页面')
  //#endif
}
```

## 样式的条件注释

代码演示

```css
/* #ifdef H5 */
view{
  height: 100px;
  line-height: 100px;
  background: red;
}
/* #endif */
/* #ifdef MP-WEIXIN */
view{
  height: 100px;
  line-height: 100px;
  background: green;
}
/* #endif */
```



# 页面跳转

## 声明式跳转

### 跳转普通页面

**默认跳转有返回前页功能**

| open-type | 类型       |
| --------- | ---------- |
| redirect  | 无返回按钮 |
| switchTab | 跳转tabbar |



```vue
<!-- [1]navigator.vue .....-->
<navigator url="../detail/detail?id=80&age=22">
    <button type="primary">跳转至详情页1</button>
</navigator>

<!-- open-type="redirect"不带返回按键返回先前页面，会关闭当前页面 -->
<navigator url="../detail/detail" open-type="redirect">
    <button type="primary">跳转至详情页2</button>
</navigator>


<!-- [2]detail.vue .....-->
<template>
	<view>
		详情页
		{{id}}
	</view>
</template>

<script>
	export default{
		onLoad(options) {
			console.log('传过来的数据',options)
		}
	}
</script>
```



效果如下：

![navigator声明跳转](http://img.mxranger.cn/Uni-App打造跨平台应用/navigator声明跳转.gif)



### 跳转tabbar

```vue
<!-- navigateTo:fail can not navigateTo a tabbar page
跳转tab页面必须设置open-type="switchTab"
-->
<navigator url="../message/message" open-type="switchTab">
    <button type="primary">跳转至信息页</button>
</navigator>
```







## 编程式调转

> [导航跳转文档]( [uni.navigateTo](https://uniapp.dcloud.io/api/router?id=navigateto))

### **利用navigateTo进行导航跳转**

保留当前页面，跳转到应用内的某个页面，使用`uni.navigateBack`可以返回到原页面。

```html
<button type="primary" @click="goAbout">跳转到关于页面</button>
```

通过navigateTo方法进行跳转到普通页面

```js
goAbout () {
  uni.navigateTo({
    url: '/pages/about/about',
  })
}
```

### **通过switchTab跳转到tabbar页面**

跳转到tabbar页面

```html
<button type="primary" @click="goMessage">跳转到message页面</button>
```

通过switchTab方法进行跳转

```js
goMessage () {
  uni.switchTab({
    url: '/pages/message/message'
  })
}
```

### **redirectTo进行跳转** 

关闭当前页面，跳转到应用内的某个页面。

```html
<!-- template -->
<button type="primary" @click="goMessage">跳转到message页面</button>
<!-- js -->
goMessage () {
  uni.switchTab({
    url: '/pages/message/message'
  })
}
```

通过onUnload测试当前组件确实卸载

```js
onUnload () {
  console.log('组件卸载了')
}
```

### 导航跳转传递参数

在导航进行跳转到下一个页面的同时，可以给下一个页面传递相应的参数，接收参数的页面可以通过onLoad生命周期进行接收

传递参数的页面

```js
goAbout () {
  uni.navigateTo({
    url: '/pages/about/about?id=80',
  });
}
```

接收参数的页面

```js
<script>
	export default {
		onLoad (options) {
			console.log(options)
		}
	}
</script>
```



# uni-app中组件的创建

## 创建

在uni-app中，可以通过创建一个后缀名为vue的文件，即创建一个组件成功，其他组件可以将该组件通过impot的方式导入，在通过components进行注册即可

+ 创建login组件，在component中创建login目录，然后新建login.vue文件

  ```
  <template>
  	<view>
  		这是一个自定义组件
  	</view>
  </template>
  
  <script>
  </script>
  
  <style>
  </style>
  ```

+ 在其他组件中导入该组件并注册

  ```
  import login from "@/components/test/test.vue"
  ```

+ 注册组件

  ```js
  components: {test}
  ```

+ 使用组件

  ```
  <test></test>
  ```

## 组件的生命周期函数

| beforeCreate  | 在实例初始化之后被调用。[详见](https://cn.vuejs.org/v2/api/#beforeCreate) |              |      |
| ------------- | ------------------------------------------------------------ | ------------ | ---- |
| created       | 在实例创建完成后被立即调用。[详见](https://cn.vuejs.org/v2/api/#created) |              |      |
| beforeMount   | 在挂载开始之前被调用。[详见](https://cn.vuejs.org/v2/api/#beforeMount) |              |      |
| mounted       | 挂载到实例上去之后调用。[详见](https://cn.vuejs.org/v2/api/#mounted) 注意：此处并不能确定子组件被全部挂载，如果需要子组件完全挂载之后在执行操作可以使用`$nextTick`[Vue官方文档](https://cn.vuejs.org/v2/api/#Vue-nextTick) |              |      |
| beforeUpdate  | 数据更新时调用，发生在虚拟 DOM 打补丁之前。[详见](https://cn.vuejs.org/v2/api/#beforeUpdate) | 仅H5平台支持 |      |
| updated       | 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。[详见](https://cn.vuejs.org/v2/api/#updated) | 仅H5平台支持 |      |
| beforeDestroy | 实例销毁之前调用。在这一步，实例仍然完全可用。[详见](https://cn.vuejs.org/v2/api/#beforeDestroy) |              |      |
| destroyed     | Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。[详见](https://cn.vuejs.org/v2/api/#destroyed) |              |      |



## 案例

### test子组件

```vue
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
```



### index主组件

```vue
<template>
	<view class="content">
		<button type="primary" @click="checkFlag">销毁组件</button>
		<!-- 加入components组件 -->
		<test v-if="flag"></test>
	</view>
</template>

<script>
	import test from '../../components/test.vue'
	
	export default {
		data() {
			return {
				flag:true
			}
		},
		methods: {
			checkFlag(){
				console.log('手动销毁')
				this.flag = false
			}
		},
		components:{//注册
			test:test
		}
	}
</script>
```

效果如下：

![组件生命周期](http://img.mxranger.cn/Uni-App打造跨平台应用/组件生命周期.gif)



# 组件的通讯

## 父组件给子组件传值

通过props来接受外界传递到组件内部的值

```
<template>
	<view>
		这是一个自定义组件 {{msg}}
	</view>
</template>

<script>
	export default {
		props: ['msg']
	}
</script>

<style>
</style>
```

其他组件在使用login组件的时候传递值

```
<template>
	<view>
		<test :msg="msg"></test>
	</view>
</template>

<script>
	import test from "@/components/test/test.vue"
	export default {
		data () {
			return {
				msg: 'hello'
			}
		},
		
		components: {test}
	}
</script>
```

## 子组件给父组件传值

通过$emit触发事件进行传递参数

```html
<template>
	<view>
		这是一个自定义组件 {{msg}}
		<button type="primary" @click="sendMsg">给父组件传值</button>
	</view>
</template>

<script>
	export default {
		data () {
			return {
				status: '打篮球'
			}
		},
		props: {
			msg: {
				type: String,
				value: ''
			}
		},
		methods: {
			sendMsg () {
				this.$emit('myEvent',this.status)
			}
		}
	}
</script>
```

父组件定义自定义事件并接收参数

```html
<template>
	<view>
		<test :msg="msg" @myEvent="getMsg"></test>
	</view>
</template>
<script>
	import test from "@/components/test/test.vue"
	export default {
		data () {
			return {
				msg: 'hello'
			}
		},
		methods: {
			getMsg (res) {
				console.log(res)
			}
		},
		
		components: {test}
	}
</script>
```



# uni-ui扩展组件

> 组件市场有很多插件，以日历组件为例

1、进入[官网](https://uniapp.dcloud.io/component/README?id=uniui )，找到日历组件，点击使用HBuilderX导入插件

![image-20200425101532176](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200425101532176.png)

2、组件自动到当前项目的components文件夹中

![image-20200425101652340](http://img.mxranger.cn/Uni-App打造跨平台应用/image-20200425101652340.png)

3、参照下面的demo使用，效果如下

![日历组件](http://img.mxranger.cn/Uni-App打造跨平台应用/日历组件.gif)