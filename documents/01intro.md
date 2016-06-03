<br>

> 修改App.js

<br>

	import React from 'react';
	
	class App extends React.Component{
	    render(){
	        return <h1>Hello World</h1>
	    }
	}
	
	export default App

<br>

> npm start

<br>

> http://localhost:8523/

<br>

> 修改App.js,使用`React.createElement`创建组件

<br>

	import React from 'react';
	
	class App extends React.Component{
	    render(){
	        return React.createElement('h1', null, 'Hello guys from jyn')
	    }
	}
	
	export default App

<br>

> 修改App.js,使用无状态函数(stateless function)的方式创建组件

<br>
	
	import React from 'react';
	
	const App = () => <h1>Hello Guys</h1>
	
	export default App

<br>

**总结：**

- 包含状态时，使用`class App extends React.Comnponent...`的方式创建组件
- 不包含状态时，使用无状态函数方式创建组件