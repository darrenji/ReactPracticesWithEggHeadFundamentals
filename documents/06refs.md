<br>

> App.js

<br>

	import React from 'react';
	
	class App extends React.Component {
	    constructor(){
	        super();
	        this.state = {txt: ''}
	        this.update = this.update.bind(this)
	    }
	    
	    update(e){
	        this.setState({txt: e.target.value})
	    }
	    
	    render(){
	        return (
	            <div>
	                {this.state.txt}
	                <hr />
	                <Slider update={this.update} />
	                <Slider update={this.update} />
	                <Slider update={this.update} />
	            </div>
	        );
	    }
	}
	
	
	class Slider extends React.Component {
	    render(){
	        return (
	            <input type="range"
	                min="0"
	                max="255"
	                onChange={this.props.update} />
	        );
	    }
	}
	
	
	
	export default App;

- Slider作为被嵌套组件，通过input的onChange事件触发`this.props.update`
- Slider被嵌套在App之内后，Slider的update属性值由App的update方法提供

<br>

> http://localhost:8523/

<br>

滑动每个滑动条，改变的是state中的txt属性值。

<br>

**是否可以滑动每个滑动条，不改变同一个state中的值呢？**

<br>

如果再渲染每个Slider组件的时候，给Slider某个属性值用来标记就可以了，就像这样：

	<Slider mark="red" update={this.update} />
	<Slider mark="green" update={this.update} />
	<Slider mark="blue" update={this.update} />

<br>

React为我们提供了**ref**属性。

> App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component {
	    constructor(){
	        super();
	        this.state = {
	            red: 0,
	            green: 0,
	            blue: 0
	        }
	        this.update = this.update.bind(this)
	    }
	    
	    update(e){
	        this.setState({
	            red: ReactDOM.findDOMNode(this.refs.red).value,
	            green: ReactDOM.findDOMNode(this.refs.green).value,
	            blue: ReactDOM.findDOMNode(this.refs.blue).value
	        })
	    }
	    
	    render(){
	        return (
	            <div>
	                <Slider ref="red" update={this.update} />
	                {this.state.red}
	                <br />
	                <Slider ref="green" update={this.update} />
	                {this.state.green}
	                <br />
	                <Slider ref="blue" update={this.update} />
	                {this.state.blue}
	                <br />
	            </div>
	        );
	    }
	}
	
	
	class Slider extends React.Component {
	    render(){
	        return (
	            <input type="range"
	                min="0"
	                max="255"
	                onChange={this.props.update} />
	        );
	    }
	}
	
	
	
	export default App;

- 被嵌套组件Slider还是原来的样子，只不过在渲染的时候加上了ref属性，这是React给到我们的
- 这些ref的属性值存到哪里了呢？--存到了this.refs.red, this.refs.green, this.refs.blue中了
- 当通过this.setState设置的时候，通过`ReactDOM.findDOMNode`找到了各自的Slider

<br>

> http://localhost:8523/

<br>

**如果Slider组件包裹在一个div中呢？**

<br>

	class Slider extends React.Component {
	    render(){
	        return (
	            <div>
	                <input type="range"
	                    min="0"
	                    max="255"
	                    onChange={this.props.update} />
	            </div>
	        );
	    }
	}

<br>

> http://localhost:8523/

<br>

效果不再了。因为，此时通过`ReactDOM.findDOMNode(this.refs.red)`找到的是包裹在input外层的div啊，div可没有value哦！

<br>

以上，在渲染Slider组件的时候用到了ref属性，实际上，还可以在定义Slider属性的时候用到ref属性：

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component {
	    constructor(){
	        super();
	        this.state = {
	            red: 0,
	            green: 0,
	            blue: 0
	        }
	        this.update = this.update.bind(this)
	    }
	    
	    update(e){
	        this.setState({
	            red: ReactDOM.findDOMNode(this.refs.red.refs.inp).value,
	            green: ReactDOM.findDOMNode(this.refs.green.refs.inp).value,
	            blue: ReactDOM.findDOMNode(this.refs.blue.refs.inp).value
	        })
	    }
	    
	    render(){
	        return (
	            <div>
	                <Slider ref="red" update={this.update} />
	                {this.state.red}
	                <br />
	                <Slider ref="green" update={this.update} />
	                {this.state.green}
	                <br />
	                <Slider ref="blue" update={this.update} />
	                {this.state.blue}
	                <br />
	            </div>
	        );
	    }
	}
	
	
	class Slider extends React.Component {
	    render(){
	        return (
	            <div>
	                <input ref="inp" type="range"
	                    min="0"
	                    max="255"
	                    onChange={this.props.update} />
	            </div>
	        );
	    }
	}
	
	
	
	export default App;

- 以上，在Slider组件内的input上加了`ref="inp"`，这个被放到了Slider组件的refs.inp中了
- 在APP组件的update方法中，通过`this.setState`改变状态，通过`ReactDOM.findDOMNode`找到元素，`this.refs.red`找到的是App组件中对应的Slider,`this.refs.red.refs.inp`找到的是Slider组件中，标有`ref="inp"`的部分

<br>

> http://localhost:8523/

<br>