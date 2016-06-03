<br>

**组件嵌套**

<br>

> 修改App.js

<br>

	import React from 'react';
	
	class App extends React.Component {
	    constructor(){
	        super();
	        this.state = {txt: 'this is the state txt'}
	        this.update = this.update.bind(this)
	    }
	    
	    update(e){
	        this.setState({txt: e.target.value})
	    }
	    
	    render(){
	        return (
	            <div>
	                <Widget txt={this.state.txt} update={this.update}/>
	            </div>
	        )
	    }
	}
	
	const Widget = (props) => {
	    return (
	        <div>
	            <input type="text"
	                onChange={props.update} />
	            <h1>{props.txt}</h1>
	        </div>
	    )
	}
	
	export default App;

- Widget作为被嵌套的组件，提供了`props.update`和`props.txt`这两个属性，用来接收外界传给它的值
- Widget被嵌套在App组件内，Widget的`props.update`属性值由App组件的update方法提供，Widget的`props.txt`属性值由App组件的`state.txt`提供
- 被嵌套组件Widget看作是河流的下游，嵌套组件App看作是是河流的上游，河水从上游流经到下游，并把上游中的state中的值以及上游中的自定义方法赋值给下游的属性`props.update`和`props.txt`

<br>

> http://localhost:8523/

<br>