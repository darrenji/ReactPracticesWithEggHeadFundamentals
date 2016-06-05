<br>

**比如，我们可以在componentWillMount事件中设置状态。**

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
	        this.setState({m: 2})
	    }
	    
	    render(){
	        console.log('rendering!')
	        return <button onClick={this.update}>{this.state.val * this.state.m}</button>
	    }
	    
	    componentDidMount(){
	        console.log('mounted');
			console.log(ReactDOM.findDOMNode(this));
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



- 在App组件的componentWillMount事件中设置了状态，然后在App组件的render方法中就可以使用刚设置的状态。
- 在App组件的componentDidMount把当前的组件DOM在控制台显示了出来

<br>

> npm start

<br>

> localhost:8523

<br>

**在componentDidMount事件中，让间歇性地执行update方法。**

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
	        this.setState({m: 2})
	    }
	    
	    render(){
	        console.log('rendering!')
	        return <button onClick={this.update}>{this.state.val * this.state.m}</button>
	    }
	    
	    componentDidMount(){
	        console.log('mounted');
	        this.inc = setInterval(this.update, 500)
	    }
	    
	    componentWillUnmount(){
	        console.log('bye');
	        clearInterval(this.inc)
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

- 在App组件的componentDidMount事件中，通过setInterval方法让其间歇性地执行App组件的update方法
- 在App组件的componentWillUnmount事件中，取消了setInterval

<br>

> npm start

<br>

> localhost:8523

<br>





