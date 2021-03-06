# 打包工具作用是什么？存在的意义？有哪些好处？

 web前端打包工具，它能将我们前端人员写得less,sass等编译成css.将多个js文件合并压缩成一个js文件。它的作用就是通过将代码编译、压缩，合并等操作，来减少代码体积，减少网络请求。以及方便在服务器上运行。目前，会使用web前端打包工具是现代前端人员必备技能。
# 准备工作
- 安装nodejs

	windows直接下载安装，linux可能自带的node版本有点低需要自己安装。

- 使用淘宝的cnpm包管理器
	由于npm的包下载源在国外，所以安装依赖包时速度可能会很慢，建议使用淘宝的cnpm，下载源在国内，所以速度很快。cnpm安装方式有两种：

	1、 npm install -g cnpm --registry=https://registry.npm.taobao.org

	直接使用npm安装，将以上命令输入到终端中即可

	2、若以上方式不行，建议移步cnpm网站使用第二种安装方式

# parcel使用
- 构建工具推荐使用parcel

	首先通过 Yarn 或者 npm 安装 Parcel ：

	- Yarn:

		 `yarn global add parcel-bundler`
	- npm:

		`npm install -g parcel-bundler`

	在你正在使用的项目目录下创建一个 package.json 文件：

		yarn init -y
	or

		npm init -y
Parcel 可以使用任何类型的文件作为入口，但是最好还是使用 HTML 或 JavaScript 文件。

	接下来，创建一个` index.html` 和 `index.js` 文件。

	Parcel 内置了一个当你改变文件时能够自动重新构建应用的开发服务器，而且为了实现快速开发，该开发服务器支持热模块替换。只需要在入口文件指出：

		parcel index.html
	现在在浏览器中打开 `http://localhost:1234/`

	具体看官网[parcel中文网](https://parceljs.org/getting_started.html)

# san使用
- 安装san

	建议直接使用网页外联js文件的方式，简单迅速。

	开发版本：

		<script src="https://unpkg.com/san@latest/dist/san.dev.js"></script>

	建议在开发环境不要用生产版本，开发版本提供了有助于开发的错误提示和警告！

	具体看官网[san官网](https://baidu.github.io/san/)
# 任务描述
- 支持js、css格式的解析

	这个parcel自带支持，webpack需要配置插件，所以如果你使用parcel就自动完成这个任务了。这里再提下parcel的优点，parcel会自动根据你引入的文件来安装所需的插件，所以如果想使用less或者其他css预处理语言，直接在网页引入相应的文件，parcel在构建时会自动处理一切事情，例如使用less
	`<link rel="stylesheet" href="./index.less">`

  	`<!-- 直接在head标签里引入less文件即可 -->`

- 区分 development / production 环境

	这里注意区分你的san文件的版本，开发时一定要使用开发版本，这样会大幅度提高你定位错误的能力。

- 使用npm scripts设罝dev、test、build命令

	这里只谈parcel的配置方法,在package.json文件里这样配置即可
	
	其中 index.html 请对应替换成你的入口文件

		"scripts": {
		  "test": "echo "Error: no test specified" && exit 1",
		  "start": "parcel index.html",
		  "dev": "npm run start",
		  "build": "parcel build index.html"
		}
- 写一个san组件并在浏览器中显示hello world

	移步[san文档](https://baidu.github.io/san/)

- 使用babel-loader进行js代码转换

	这里只介绍parcel的使用方法，对比webpack来说，真是灰常简单

	使用npm或者cnpm安装babel-preset-env即在终端中输入以下命令

		npm i -D babel-preset-env 

	然后在与package.json文件相同目录下新建一个文件名为 .babelrc 的文件并输入以下配置，parcel便会在构建时自动配置


		{
		  "presets": [
		      "env"
		  ]
		}

# 注意引入script的位置
错误的引入位置：

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>hello world</title>
	    <script src="https://unpkg.com/san@latest/dist/san.dev.js"></script>
	        <script src="./index.js"></script>
	</head>
	<body>
	</body>
</html>
正确的引入位置与顺序：

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>hello world</title>
	    <script src="https://unpkg.com/san@latest/dist/san.dev.js"></script>
	</head>
	<body>
	    <script src="./index.js"></script>
	</body>
	</html>