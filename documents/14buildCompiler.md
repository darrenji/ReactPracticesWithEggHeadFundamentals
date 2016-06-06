<br>

**本篇体验使用babel把jsx转换成js现实出来。**

<br>

在文本框中输入jsx代码，触发组件的update事件，适时地把jsx转换成js代码现实出来。

<br>

> style.css,在根目录下创建

<br>

	body {
	  margin: 0;
	  padding: 0;
	  font-family: monospace;
	}
	
	header {
	  display: block;
	  height: 5vh;
	  overflow: auto;
	  background-color: pink;
	  color: red;
	  font-size: 28px
	}
	
	.container {
	  height: 95vh;
	  display:flex;
	}
	
	pre {
	  background-color: #f8f8f8;
	}
	
	pre, textarea {
	  width: 50%;
	  font-family: monospace;
	  font-size: 28px;
	  margin: 0;
	  padding: 10px;
	  color: #222;
	}
	
	textarea:focus {outline: 0;}

<br>

> index.html

<br>

	<!doctype html>
	<html>
	<head>
	    <meta charset="UTF-8">
	    <title>Untitled Document</title>
	    <link rel="stylesheet" href="/node_modules/bootstrap/dist/css/bootstrap.css">
	    <link rel="stylesheet" href="style.css">
	    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.33/browser.js"></script>
	</head>
	<body>
	
	<div id="app"></div>
	<script src="index.js"></script>
	</body>
	</html>

<br>

> App.js

<br>

	import React from 'react';
	
	class App extends React.Component {
	  constructor(){
	    super();
	    this.state = {
	      input: '/* add your jsx here */',
	      output: '',
	      err: ''
	    }
	    this.update = this.update.bind(this);
	  }
	  update(e){
	    let code = e.target.value;
	    try {
	      this.setState({
	        output: babel.transform(code, {
	          stage: 0,
	          loose: 'all',
	          comments: true
	        }).code,
	        err: ''
	      })
	    }
	    catch(err){
	      this.setState({err: err.message})
	    }
	
	  }
	  render(){
	    return (
	      <div>
	        <header>{this.state.err}</header>
	        <div className="container">
	          <textarea
	            onChange={this.update}
	            defaultValue={this.state.input}>
	            </textarea>
	          <pre>
	            {this.state.output}
	          </pre>
	        </div>
	      </div>
	    )
	  }
	}
	
	export default App

- App组件的defaultValue属性值来自于state
- App组件用来显示错误信息的来自`this.state.err`
- App组件用来显示js代码的来自`this.state.output`
- App组件中textarea的onChange事件触发update方法，其内部使用`babel.transform`把jsx转换成js代码

<br>

> npm start

<br>

> localhost:8523

<br>





