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

### checkbox - intermediate state

[intermediate state can only be set with javascript](https://css-tricks.com/indeterminate-checkboxes/) 

```js
var checkbox = document.getElementById("some-checkbox");
checkbox.indeterminate = true;
```

### `patch` command

`patch < patch-file`

for example 

```
吽 echo hi\\nhello > 1.txt

吽 echo Hi\\nHello > 2.txt

吽 diff -u 1.txt 2.txt > patch.txt
[zsh] sabandyo at sabandyo-mn1 in ~ 

吽 cat 1.txt
hi
hello

吽 cat patch.txt 
--- 1.txt	2016-03-24 18:56:38.000000000 -0700
+++ 2.txt	2016-03-24 18:56:32.000000000 -0700
@@ -1,2 +1,2 @@
-hi
-hello
+Hi
+Hello

吽 patch < patch.txt 
patching file 1.txt

吽 cat 1.txt        
Hi
Hello
```

### `[` vs `[[`

* `[[`
  * is more powerful
  * is only supported in modern `shell` like `bash`, `zsh`
  * is not available in `POSIX shells`
  * is safer
  * use `#!/bin/bash` or `#!/bin/zsh` when using `[[`
  
* `[`
  * `var`s containing `spaces` nedds to be wrapped in `"`

More information can be found at this [StackOverflow answer](http://stackoverflow.com/questions/13542832/what-is-the-difference-between-single-and-double-square-brackets-in-bash#answer-31366734)

### modify an older (not latest) commit message

* `git rebase -i HEAD~10` for example if the 10th commit from the latest needs to be modified
* replace `pick` with `edit` for the corresponding commit
* `git commit --amend`
* update the commit message
* `git rebase --continue

### `matching` vs `current` `push.default` in `git`

* `matching` means `git push` will `push` **all local branches**, to the ones with the same name on the remote. This makes it easy to accidentally push a non-intended branch.

* `simple` means `git push` will push **only the current branch**, to the one that `git pull` would pull from, and also checks that their names match. This is a more intuitive behavior, which is why the default is getting changed to this.

### `node filename` is sufficient `.js` is not required

### `<button>` is better than `<a>` for custom widgets

* `<a> must be accompanied with `href` `attribute`
  * otherwise `click` handler would not listen to `enter` press
  * and it will not be focusable with `tab`
* `<a>` does not respect `space` press (at least in chrome/safari/firefox on Mac)
* for `<a>`, `e.prevenDefault()` must be used in the `click` handler
* both of them need to have widget `role` attribute, if not serving the native semantic

### Vim - save a file with `sudo`

_I haven't learnt this today, but I keep forgetting it_

```
w !sudo tee %
```
