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
