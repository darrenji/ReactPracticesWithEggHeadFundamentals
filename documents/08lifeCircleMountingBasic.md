<br>

本篇体验React生命周期事件的基础部分。

<br>

> 修改App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    constructor(){
	        super();
	        this.state = {val: 0};
	        this.update = this.update.bind(this);
	    }
	    
	    update(){
	        this.setState({val: this.state.val + 1})
	    }
	    
	    render(){
	        console.log('rendering!')
	        return <button onClick={this.update}>{this.state.val}</button>
	    }
	}
	
	
	export default App;

<br>

> npm start

<br>

> localhost:8523

<br>

**接着体验更多的React生命周期事件。**

<br>

> App.js

<br>


	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    constructor(){
	        super();
	        this.state = {val: 0};
	        this.update = this.update.bind(this);
	    }
	    
	    update(){
	        this.setState({val: this.state.val + 1})
	    }
	    
	    componentWillMount(){
	        console.log('mounting')
	    }
	    
	    render(){
	        console.log('rendering!')
	        return <button onClick={this.update}>{this.state.val}</button>
	    }
	    
	    componentDidMount(){
	        console.log('mounted');
	    }
	    
	    componentWillUnmount(){
	        console.log('bye');
	    }
	}
	
	class Wrapper extends React.Component {
	    constructor(){
	        super();
	    }
	    
	    mount(){
	        ReactDOM.render(<App />, document.getElementById('a'))
	    }
	    
	    unmount(){
	        ReactDOM.unmountComponentAtNode(document.getElementById('a'))
	    }
	    
	    render(){
	        return (
	            <div>
	                <button onClick={this.mount.bind(this)}>Mount</button>
	                <button onClick={this.unmount.bind(this)}>Unmount</button>
	                <div id="a"></div>
	            </div>
	        )
	    }
	}
	
	
	export default Wrapper;

- 这次导出的是Wrapper这个组件
- 页面渲染，首先显示Mount和Unmount这2个按钮
- 点击Mount按钮，就把App组件渲染出来，经历了componentWilMount, render, componentDidMount事件
- 点击Unmount按钮，用到了`ReactDOM.unmountComponentAtNode`把App组件从DOM上卸载下来，经历了App组件的componentWillUnmount事件

<br>

> npm start

<br>

> localhost:8523

<br>


