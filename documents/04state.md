<br>

**组件除了可以从属性中获取到值，还可以从哪里获取到值呢？** --还可以从state中获取到值。

<br>

> 修改App.js

<br>

	import React from 'react';
	
	class App extends React.Component {
	    constructor(){
	        super();
	        this.state = {txt: 'this is the state txt'}
	    }
	    
	    render(){
	        return <h1>{this.state.txt}</h1>
	    }
	}
	
	export default App;

- constructor构造函数中的super方法也是必须的
- 组件的状态放在了this.state中了

<br>

> 修改main.js

<br>

	import React from 'react';
	import App from './App';
	import ReactDOM from 'react-dom';
	
	ReactDOM.render(<App />, document.getElementById('app'));

注意：这里虽然没有用到React，但如果去掉React是会报错的，因为在渲染组件的时候用到了React的某些方法。

<br>

> http://localhost:8523/

<br>

**如何更改状态呢？**

<br>

> 修改App.js

<br>

	import React from 'react';
	
	class App extends React.Component {
	    constructor(){
	        super();
	        this.state = {txt: 'this is the state txt'}
	    }
	    
	    update(e){
	        this.setState({txt: e.target.value})
	    }
	    
	    render(){
	        return (
	            <div>
	                <input type="text" 
	                    onChange={this.update.bind(this)} />
	                <h1>{this.state.txt}</h1>
	            </div>
	        )
	    }
	}
	
	export default App;

- 通过`this.setState`来更改状态
- update是组件的自定义方法，由input的onChange事件触发
