<br>

> App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    constructor(){
	        super();
	        this.update = this.update.bind(this);
	        this.state = {val:0};
	    }
	    
	    update(){
	        this.setState({val: this.state.val + 1})
	    }
	    
	    componentWillMount(){
	        console.log('will mount')
	    }
	    
	    render(){
	        return (
	            <button onClick={this.update}>
	                {this.props.txt} - {this.state.val}
	            </button>
	        )
	    }
	    
	    componentDidMount(){
	        console.log('mounted')
	    }
	}
	
	App.defaultProps = {txt: 'button'}
	
	
	
	export default App;

- 通过defaultProps设置了this.props.txt
- 点击按钮就执行组件的update方法，重新设置状态

<br>

> npm start

<br>

> localhost:8523

<br>

以上，在页面上显示了如下：

	<button onClick={this.update}>
	    {this.props.txt} - {this.state.val}
	</button>

<br>

如果，在页面上，除了以上，还想显示如下：

	<label
	    onMouseOver={props.update}>
	        {props.txt} - {props.val}
	</label>

<br>

虽然，一个是button，一个是label,但两者接受数据的方式是一样的。这时候就可以引出**mixin**模式了。

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	
	let Mixin = InnerComponent => class extends React.Component{
	    constructor(){
	        super();
	        this.update = this.update.bind(this);
	        this.state = {val: 0}
	    }
	    
	    update(){
	        this.setState({val: this.state.val + 1})
	    }
	    
	    componentWillMount(){
	        console.log('will mount')
	    }
	    
	    render(){
	        return <InnerComponent
	            update={this.update}
	            {...this.state}
	            {...this.props} />
	    }
	    
	    componentDidMount(){
	        console.log('mounted')
	    }
	}
	
	
	const Button = (props) => <button
	                            onClick={props.update}>
	                                {props.txt} - {props.val}
	                            </button>
	                            
	const Label = (props) => <label
	                            onMouseOver={props.update}>
	                                {props.txt} - {props.val}
	                        </label>
	                            
	                            
	let ButtonMixed = Mixin(Button);
	let LabelMixed = Mixin(Label);
	                            
	class App extends React.Component{
	    render(){
	        return (
	            <div>
	                <ButtonMixed txt="Button" />
	                <LabelMixed txt="Label" />
	            </div>
	        )
	    }
	}
	
	
	export default App;

- 首先，有了Button和Label组件，虽然表现不一样，但接受数据的方式相似
- 然后把Button和Label传给Mixin这个组件，接受其中的数据，再把Button和Label组件显示出来

<br>

> npm start

<br>

> localhost:8523

<br>






