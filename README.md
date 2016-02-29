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
