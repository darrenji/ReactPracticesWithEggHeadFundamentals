<br>

**本篇体验jsx和js之间的对应关系。**

<br>

> 使用无状态函数、Lambda表达式创建jsx

<br>

	//jsx
	const App = (props) => {
		return (
			<div></div>
		)
	}

	//js
	"use strict";

	var App = function App(props){
		return React.createElement("div", null);
	}

- `<div></div>`可以写成`<div />`
	
<br>

> 组件中有组件

<br>

	//jsx
	const App = (props) => {
		return (
			<App></App>
		)
	}

	//js
	"use strict";

	var App = function App(props){
		return React.createElement(App, null);
	}
- `<App></App>`可以写成`<App />`

<br>

> 创建组件的时候没有包裹元素

<br>

	//jsx
	const App = (props) => {
		return (
			<App />
			<App />
		)
	}

	//报错：Adjacent JSX elments must be wrapped in an enclosing tag

<br>

正确的写法是：

<br>

	//jsx
	const App = (props) => {
		return (
			<div>
				<App />
				<App />
			</div>
		)
	}

	//js
	"use strict";

	var App = function App(props){
		return React.createElement(
			"div",
			null,
			React.createElement(App, null),
			React.createElement(App, null)
		);
	}

<br>

> 组件的属性，在jsx中是怎样的？

<br>

	//jsx
	const App = (props) => {
		return (
			<div>
				<a href="#" notrendered="x"></a>
			</div>
		)
	}

	//js
	"use strict";

	var App = function App(props){
		return React.createElement(
			"div",
			null,
			React.createElement("a", {href: "#", notrendered: "x"})
		);
	}

可见，组件的属性都作为了`React.createElement`方法第二个实参对象的键。

<br>


