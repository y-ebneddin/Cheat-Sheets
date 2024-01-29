# React

## Philosophy
- Component Base
- Composition is better than inheritance
- Simplicity, Unopinionated
- Fast development and high testability
- Hase a good ecosystem and community
- Declarative insted of Imperative

#### Declarative vs. Imperative
```javascript
// Imperative
let arr = [1,2,3,4,5],arr2 = [];
for (var i=0;i<arr.length;i++){
	arr2[i] = arr[i]*2;
}

// Declarative
let arr = [1,2,3,4,5];
arr2 = arr.map(function(v,i){
	return v*2;
});
```

## Simple React
####  React without JSX
```html
<body>
	<div id="root"></div>
	<script>
		class Hello extends React.Component {
		  render() {
			return React.createElement('div', null, `Hello ${this.props.toWhat}`);
		  }
		}
		const root = ReactDOM.createRoot(document.getElementById('root'));
		root.render(React.createElement(Hello, {toWhat: 'World'}, null));
	</script>
</body>
```
####  React with JSX
```javascript
import React from 'react'
import ReactDOM from 'react-dom'
function App() {
  return 'Hello'
}
ReactDOM.render(<App />, document.getElementById('root'))
```

** Notes: **
- Each function is a component
- Each function have to return one HTML tag.
- For returning multi elements we use <> ... <\> tags as container.
- We use { } expretion to binding a variable

## History
- JavaScript: Function base
- Module System: CommonJS | AMD | EQMAScript (ES6)
- Module bundle: RequireJS | SystemJS | RollupJS
- JavaScript Task Runner: Grunt | Gulp (Pipeline)
- Application Bundler: Webpack (Like assemble) | Parcel (Zero config) | Vite 


[The JavaScript Modules Handbook – Complete Guide to ES Modules and Module Bundlers](https://www.freecodecamp.org/news/javascript-es-modules-and-module-bundlers/#common-types-of-module-systems-in-javascript "The JavaScript Modules Handbook – Complete Guide to ES Modules and Module Bundlers")

## First project
