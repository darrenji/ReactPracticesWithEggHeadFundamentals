<br>

参考：https://github.com/joemaddalone/egghead-react-fundamentals-es6/tree/master/lessons


<br>

> npm init

<br>

> npm install react react-dom --save

<br>

> npm install babel-loader babel-core babel-preset-es2015 babel-preset-react --save

<br>

> touch index.html App.js main.js webpack.config.js

<br>

> npm install babel webpack webpack-dev-server -g

<br>

> 配置webpack.confgi.js文件

<br>

	module.exports = {
	  entry: './main.js',
	  output: {
	    path: './',
	    filename: 'index.js'
	  },
	  devServer: {
	    inline: true,
	    port: 8523
	  },
	  module: {
	    loaders: [
	      {
	        test: /\.js$/,
	        exclude: /node_modules/,
	        loader: 'babel',
	        query: {
	          presets: ['es2015', 'react']
	        }
	      }
	    ]
	  }
	}

babel用来把ES6转换成ES5，JSX转换成JS。

<br>

> index.html，在这里呈现页面

<br>

	<!doctype html>
	<html>
	<head>
	    <meta charset="UTF-8">
	    <title>Untitled Document</title>
	</head>
	<body>
	
	<div id="app"></div>
	<script src="index.js"></script>
	</body>
	</html>

<br>

> App.js,在这里定义组件

<br>

	import React from 'react';
	
	class App extends React.Component{
	    render(){
	        return <div>Hello</div>
	    }
	}
	
	export default App

<br>

> main.js,在这里把组件渲染到DOM上

<br> 

	import React from 'react';
	import ReactDOM from 'react-dom';
	import App from './App';
	
	ReactDOM.render(<App />, document.getElementById('app'))

<br>

> package.json, 在这里配置一个npm命令

<br>

	{
	  "name": "fundamental",
	  "version": "1.0.0",
	  "description": "",
	  "main": "index.js",
	  "scripts": {
	    "start": "webpack-dev-server"
	  },
	  "author": "",
	  "license": "ISC",
	  "dependencies": {
	    "react": "^15.1.0",
	    "react-dom": "^15.1.0",
	    "babel-core": "^6.9.1",
	    "babel-loader": "^6.2.4",
	    "babel-preset-es2015": "^6.9.0",
	    "babel-preset-react": "^6.5.0"
	  }
	}

<br>

> npm start

<br>

注意：每次运行npm start如果不及时关掉(`ctrl + c`),会报如下错：

<br>

	npm ERR! windows_NT 10.0.10240
	npm ERR! npm-cli.js
	webpack-dev-server not with npm

<br>

> 浏览器：localhost:8523

<br>







