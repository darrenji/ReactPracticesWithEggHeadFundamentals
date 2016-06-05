<br>

> App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    constructor(){
	        super();
	        this.update = this.update.bind(this);
	    }
	    
	    update(){
	        ReactDOM.render(
	            <App val={this.props.val + 1} />,
	            document.getElementById('app')
	        )
	    }
	    
	    render(){
	        return (
	            <button onClick={this.update}>
	                {this.props.val}
	            </button>
	        )
	    }
	}
	
	App.defaultProps = {val: 0}
	
	
	export default App;

- 通过defaultProps属性给到了一个初始值
- 点击按钮的时候，调用`ReactDOM.render`方法重新渲染App组件，并给val属性设置新的值

<br>

**其实，在App这个组件通过val属性接受值并更新这个过程中，可以有更细粒度的控制。**

<br>

> App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    constructor(){
	        super();
	        this.update = this.update.bind(this);
	        this.state = {increasing: false}
	    }
	    
	    update(){
	        ReactDOM.render(
	            <App val={this.props.val + 1} />,
	            document.getElementById('app')
	        )
	    }
	    
	    componentWillReceiveProps(nextProps){
	        this.setState({increasing: nextProps.val > this.props.val})
	    }
	    
	    shouldComponentUpdate(nextProps, nextState){
	        return nextProps.val % 5 === 0;
	    }
	    
	    render(){
	        console.log(this.state.increasing)
	        return (
	            <button onClick={this.update}>
	                {this.props.val}
	            </button>
	        )
	    }
	    
	    componentDidUpdate(prevProps, prevState){
	        console.log('prevProps', prevProps)
	    }
	}
	
	App.defaultProps = {val: 0}
	
	
	export default App;

- 通过`App.defaultProps`设置的值，实际是放到了`this.props.val`中了
- 在构造函数中，设置了状态，increasing为false
- shouldComponentUpdate事件决定组件是否接受属性值后更新
- componentWillReceiveProps事件是在组件接受属性值前发生
- componentDidUpdate事件是在组件接受属性值后发生

<br>

> npm start

<br>

> localhost:8523

<br>

