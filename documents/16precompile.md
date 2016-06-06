<br>

**本篇体验使用babel的命令行来编译jsx。也就是预编译，不是运行时编译。**

<br>

> src.js, 在根目录下创建

<br>

	"use strict"
	
	const App = () => {
	    return (
	        <div>Hello</div>
	    )
	}

<br>

> npm i babel-cli -g

<br>

> babel --presets react src.js -o dist.js --watch

<br>

在项目根目录项多了个一个dist.js文件：

	"use strict";
	
	const App = () => {
	    return React.createElement(
	        "div",
	        null,
	        "Hello"
	    );
	};

并且，改变src.js中的并保存，dist.js也会有相应的变化。

<br>





