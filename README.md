# today-i-learned

Today, I learned ...

### `this` in javascript anonymous function

If using `'use strict';` it's `undefined` other wise *global* `this`, `Window` in browser.

```js
(function() {
  'use strict';
  console.log(this); // undefined
}());

(function() {
  console.log(this); //[object global]
}());
```

However, in ES2015 arrow function, `this` is the lexical `this`.

### `position:relative`

* `position:relative` means the `position` of the `element` is **relative to itself**
* if there are no associated, `left`, `right`, `top`, `bottom`, `position:relative` does not have any effect for the element's layout
* unlike `position:absolute|fixed`, the element is not taken out of the flow.
* [codepen example](http://codepen.io/anon/pen/vGYPLM)

### `==` equality & value conversion in javascript

* in `==` both the values are converted into a common type prior comparison.
* for `number == string` or `string == number` `string` is convereted to `number`
* more conversion rules can be found [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#Loose_equality_using)

### `:nth-child(odd)` & `:nth-child(even)`

* `:nth-child(2n + 1)` is same as `:nth-child(odd)`
* `:nth-child(2n)` is same as `:nth-child(even)`

### `{this.props.children}` pass a react component to another 

```js
export default class Dumb extends React.Component {
  render() {
    return (
      <div>
        Hi from Dumb
        {this.props.children}
      </div>
    );
  }
}

export default class AnotherDumb extends React.Component {
  render() {
    return <span>Hello from AnotherDumb</span>;
  }
}

ReactDOMServer.renderToStaticMarkup(<Dumb><AnotherDumb /></Dumb>);
// or
ReactDOMServer.renderToStaticMarkup(
  React.createElement(
    Dumb, {}, React.createElement(AnotherDumb)
  )
);
```

```html
<div>
  Hi from Dumb
  <span>
    Hello from AnotherDumb
  </span>
</div>
```

### use `Host` to identify which `id_rsa.pub` is to be used.

```sh
Host *.example.one*
	IdentityFile 	%d/.ssh/id_rsa_example_one.pub

Host *.example.two*
	IdentityFile 	%d/.ssh/id_rsa_example_two.pub
```

### `defer` & `async` in `<script>`

* when `async` attribute is present, the script is fetched w/o blocking HTML parsing and executed as soon as it is available. While executing the HTML parsing will be blocked.
* when `defer` attribute is present, w/o `async` the script will be fetched w/o blocking HTML parsing and only executed, when the page has finished parsing. 
* without `async` or `defer`, the script is fetched blocking the HTML parsing and executed immediately.
* When `async` and `defer` both are present `defer` serves as a fall back for the browsers that don't understand `async`.
