# today-i-learned

Today, I learned ...

## `this` in javascript anonymous function

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

## `position:relative`

* `position:relative` means the `position` of the `element` is **relative to itself**
* if there are no associated, `left`, `right`, `top`, `bottom`, `position:relative` does not have any effect for the element's layout
* unlike `position:absolute|fixed`, the element is not taken out of the flow.
* [codepen example](http://codepen.io/anon/pen/vGYPLM)

## `==` equality & value conversion in javascript

* in `==` both the values are converted into a common type prior comparison.
* for `number == string` or `string == number` `string` is convereted to `number`
* more conversion rules can be found [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#Loose_equality_using)

## `:nth-child(odd)` & `:nth-child(even)`

* `:nth-child(2n + 1)` is same as `:nth-child(odd)`
* `:nth-child(2n)` is same as `:nth-child(even)`

## `{this.props.children}` pass a react component to another 

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

## use `Host` to identify which `id_rsa.pub` is to be used.

```sh
Host *.example.one*
	IdentityFile 	%d/.ssh/id_rsa_example_one.pub

Host *.example.two*
	IdentityFile 	%d/.ssh/id_rsa_example_two.pub
```

## `defer` & `async` in `<script>`

* when `async` attribute is present, the script is fetched w/o blocking HTML parsing and executed as soon as it is available. While executing the HTML parsing will be blocked.
* when `defer` attribute is present, w/o `async` the script will be fetched w/o blocking HTML parsing and only executed, when the page has finished parsing. 
* without `async` or `defer`, the script is fetched blocking the HTML parsing and executed immediately.
* When `async` and `defer` both are present `defer` serves as a fall back for the browsers that don't understand `async`.

## checkbox - intermediate state

[intermediate state can only be set with javascript](https://css-tricks.com/indeterminate-checkboxes/) 

```js
var checkbox = document.getElementById("some-checkbox");
checkbox.indeterminate = true;
```

## `patch` command

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

## `[` vs `[[`

* `[[`
  * is more powerful
  * is only supported in modern `shell` like `bash`, `zsh`
  * is not available in `POSIX shells`
  * is safer
  * use `#!/bin/bash` or `#!/bin/zsh` when using `[[`
  
* `[`
  * `var`s containing `spaces` nedds to be wrapped in `"`

More information can be found at this [StackOverflow answer](http://stackoverflow.com/questions/13542832/what-is-the-difference-between-single-and-double-square-brackets-in-bash#answer-31366734)

## modify an older (not latest) commit message

* `git rebase -i HEAD~10` for example if the 10th commit from the latest needs to be modified
* replace `pick` with `edit` for the corresponding commit
* `git commit --amend`
* update the commit message
* `git rebase --continue

## `matching` vs `current` `push.default` in `git`

* `matching` means `git push` will `push` **all local branches**, to the ones with the same name on the remote. This makes it easy to accidentally push a non-intended branch.

* `simple` means `git push` will push **only the current branch**, to the one that `git pull` would pull from, and also checks that their names match. This is a more intuitive behavior, which is why the default is getting changed to this.

## `node filename` is sufficient `.js` is not required

## `<button>` is better than `<a>` for custom widgets

* `<a> must be accompanied with `href` `attribute`
  * otherwise `click` handler would not listen to `enter` press
  * and it will not be focusable with `tab`
* `<a>` does not respect `space` press (at least in chrome/safari/firefox on Mac)
* for `<a>`, `e.prevenDefault()` must be used in the `click` handler
* both of them need to have widget `role` attribute, if not serving the native semantic

Refer this [CodePen](http://codepen.io/anon/pen/aNKWBd?editors=1111)

## Vim - save a file with `sudo`

_I haven't learnt this today, but I keep forgetting it_

```
w !sudo tee %
```

## `document.createElementNS`

`document.createElementNS(namespaceURI, qualifiedName);` creates an element with the specified namespace URI and qualified name.
For example `document.createElementNS('http://www.w3.org/2000/svg', 'svg')`

## Override a node module's function

```js
// fs.js
const fs = require('fs');
const readFileSync = fs.readFileSync;

fs.readFileSync = (...args) => {
  const content =  readFileSync.apply(null, args);
  console.log(`read ${args[0]} in sync`)
  console.log(`constent of ${args[0]}\n----------------------\n${content}`);
  return content;
}
```

```js
// app.js
const fs = require('fs');
require('./fs');

fs.readFileSync('./fs.js', 'utf-8');
```
```
$ node app.js
read ./fs.js in sync
constent of ./fs.js
----------------------
const fs = require('fs');
const readFileSync = fs.readFileSync;

fs.readFileSync = (...args) => {
  const content =  readFileSync.apply(null, args);
  console.log(`read ${args[0]} in sync`)
  console.log(`constent of ${args[0]}\n----------------------\n${content}`);
  return content;
}
```

## `npm ls <package-name>` to list the dependency tree

```sh
$ npm ls trim
...
└─┬ doctoc@1.0.0
  └─┬ markdown-to-ast@3.0.7
    └─┬ mdast@1.2.0
      └── trim@0.0.1
```

## `:after` & `:before` can not be used for `input` element

[It's not meant to be used on replaced elements such as form elements (inputs) and image elements.](http://stackoverflow.com/questions/2587669/can-i-use-the-after-pseudo-element-on-an-input-field#answer-2591460)

## start a `ordered list` from a desired ordinal value

use [`value`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li#Attributes) and [`start`](https://html.spec.whatwg.org/multipage/semantics.html#attr-ol-start) attribute

```html
<ol>
  <li start="4" value="4">item 4</li>
  <li>item 5</li>
  <li>item 6</li>
</ol>
```

## `!important` in a keyframe

[declarations in a keyframe that are qualified with !important are ignored](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes#!important_in_a_keyframe)

## `outline-offset`

`outline-offset` is a thing! and it can have `-ve` value

## `border` and `outline` styles can not be animated

This is by design, read more at [this stackoverflow answer](http://stackoverflow.com/questions/14385422/why-dont-css3-animations-work-on-outline-with-default-none#answer-14386672)

## listen to `focus` and `blur` during capture phase

`focus` & `blur` event don't bubble up. So event listener attached to the ancestor can not listen to `focus` and `blur` event on its `descendant` as it can for `click` event.

```js
document.addEventListener('click', () => {console.log(e.target, 'is clicked')}); // logs the element clicked
document.addEventListener('focus', () => {console.log(e.target)}); // however, this does not work
document.addEventListener('focus', () => {console.log(e.target)}, true); // but, this work
```

Note the `true` flag passed as the 3rd argument, in the last statement. `true` identifies it to be `capture` phase.

## remove all the untracked files

`git clean -fd` will remove all the untracked files

## element.closest()

Native [method](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest), [not jQuery](https://api.jquery.com/closest/), that returns the closest ancestor of the current element.
