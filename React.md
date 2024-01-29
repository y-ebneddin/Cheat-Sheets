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

## React without JSX
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
