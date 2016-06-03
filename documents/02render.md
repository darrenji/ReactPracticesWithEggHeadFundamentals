<br> 

> 修改App.js

<br>

	import React from 'react';
	
	class App extends React.Component{
	    render(){
	        return <h1>Hello</h1><b>World</b>
	    }
	}
	
	export default App

以上，会报错：Adjacent JSX elements must be wrapped in an enclosing tag.也就是说：render方法返回的必须包裹在一个标签中。

<br>

> 继续修改App.js,解决上面的问题

<br>

	import React from 'react';
	
	class App extends React.Component{
	    render(){
	        return (
	            <div>
	                <h1>Hello</h1>
	                <b>World</b>
	            </div>
	        );
	        
	    }
	}
	
	export default App

<br>

> 继续修改App.js,如果把return之后的括号去掉呢？

<br>

	import React from 'react';
	
	class App extends React.Component{
	    render(){
	        return 
	            <div>
	                <h1>Hello</h1>
	                <b>World</b>
	            </div>
	        
	        
	    }
	}
	
	export default App

以上，会报错：Uncaught Invariant Violation: App.render(): A valid React element (or null) must be returned. You may have returned undefined, an array or some other invalid object.所以，括号还是不能省略的。