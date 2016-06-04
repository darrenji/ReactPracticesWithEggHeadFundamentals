<br>

本篇熟悉`this.props.children`这个属性，是用来把某个组件内的其它嵌套子组件以及内容显示出来。

<br>

> npm install bootstrap --save

<br>

> 修改index.html

<br>

	<!doctype html>
	<html>
	<head>
	    <meta charset="UTF-8">
	    <title>Untitled Document</title>
	    <link rel="stylesheet" href="/node_modules/bootstrap/dist/css/bootstrap.css">
	</head>
	<body>
	
	<div id="app"></div>
	<script src="index.js"></script>
	</body>
	</html>

<br>

> 修改App.js

<br>

	import React from 'react';
	
	
	class App extends React.Component {
	    render(){
	        return <Button>I <Heart /> React</Button>
	    }
	}
	
	class Button extends React.Component{
	    render(){
	        return <button>{this.props.children}</button>
	    }
	}
	
	
	const Heart = () => <span className="glyphicon glyphicon-heart"></span>
	
	
	export default App;

- Heat组件是用无状态函数的形式写的
- Button组件中使用到了`this.props.children`，意思是说把`<button></button>`之间的组件和内容都显示出来
- 最后来到App组件，把Button组件内的内容全都显示了出来

<br>

> npm start

<br>

> http://localhost:8523/

<br>