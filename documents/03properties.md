<br>

**React组件的属性是如何添加的呢？**其实和html元素一样。

<br>

> 修改App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    render(){
	        return <h1>{this.props.txt}</h1>
	    }
	}
	
	ReactDOM.render(
	    <App txt="this is the props text" />,
	    document.getElementById('app')
	);
	
	export default App;

- 这里的txt就是组件App的属性
- 外界传入的属性值，被保存在`this.props`对象中

<br>

> 修改main.js

<br>


	import App from './App';

<br>

> http://localhost:8523/

<br>

> 修改App.js,一个更接近常态的写法

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    render(){
	        let txt = this.props.txt;
	        return <h1>{txt}</h1>
	    }
	}
	
	ReactDOM.render(
	    <App txt="this is the props text" />,
	    document.getElementById('app')
	);
	
	export default App;

<br>

**如何对组件的属性进行约束呢？**

<br>

> 修改App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    render(){
	        let txt = this.props.txt;
	        let cat = this.props.cat;
	        return <h1>{txt}{cat}</h1>
	    }
	}
	
	App.propTypes = {
	    txt: React.PropTypes.string,
	    cat: React.PropTypes.number.isRequired
	}
	
	ReactDOM.render(
	    <App cat={5} txt="this is the props text" />,
	    document.getElementById('app')
	);
	
	export default App;

以上，通过`App.propTypes`对组件属性进行约束。

<br>

**组件的属性值可以有默认的吗？**

<br>

> 修改App.js

<br>

	import React from 'react';
	import ReactDOM from 'react-dom';
	
	class App extends React.Component{
	    render(){
	        let txt = this.props.txt;
	        let cat = this.props.cat;
	        return <h1>{txt}{cat}</h1>
	    }
	}
	
	App.propTypes = {
	    txt: React.PropTypes.string,
	    cat: React.PropTypes.number.isRequired
	}
	
	App.defaultProps = {
	    txt: 'this is default txt'
	}
	
	ReactDOM.render(
	    <App cat={5} />,
	    document.getElementById('app')
	);
	
	export default App;

以上，通过`defaultProps`设置默认属性值。

<br>



