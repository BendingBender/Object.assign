#Object.assign

<!--
[![Build Status][travis-svg]][travis-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]

[![browser support][testling-png]][testling-url]
-->

An Object.assign shim. Works in browsers and node/io.js. Shims only when necessary.

Takes a minimum of 2 arguments: `target` and `source`.
Takes a variable sized list of source arguments - at least 1, as many as you want.
Throws a TypeError if the `target` argument is `null` or `undefined`.

Most common usage:

In node/io.js:

```js
require('object.assign');
```

In a browser:

```html
<script src="object.assign/index.js"></script>
```

## Example

```js
// Multiple sources!
var target = { a: true };
var source1 = { b: true };
var source2 = { c: true };
var sourceN = { n: true };

var expected = {
	a: true,
	b: true,
	c: true,
	n: true
};

require('object.assign');
var assert = require('assert');

Object.assign(target, source1, source2, sourceN);
assert.deepEqual(target, expected); // AWESOME!
```

```js
require('object.assign');
var assert = require('assert');
var target = {
	a: true,
	b: true,
	c: true
};
var source1 = {
	c: false,
	d: false
};
var sourceN = {
	e: false
};

var assigned = Object.assign(target, source1, sourceN);
assert.equal(target, assigned); // returns the target object
assert.deepEqual(assigned, {
	a: true,
	b: true,
	c: false,
	d: false,
	e: false
});
```

```js
var assert = require('assert');
/* when Object.assign is not present */
delete Object.assign;
require('object.assign');
assert.equal(typeof Object.assign, "function");

var target = {
	a: true,
	b: true,
	c: true
};
var source = {
	c: false,
	d: false,
	e: false
};

var assigned = assign(target, source);
assert.deepEqual(Object.assign(target, source), assign(target, source));
```

```js
var assert = require('assert');
/* when Object.assign is present */
var builtinAssign = Object.assign || function(){};
Object.assign = builtinAssign;
require('object.assign');
assert.equal(builtinAssign, Object.assign);

var target = {
	a: true,
	b: true,
	c: true
};
var source = {
	c: false,
	d: false,
	e: false
};

assert.deepEqual(Object.assign(target, source), assign(target, source));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

<!--
[travis-svg]: https://travis-ci.org/ljharb/object.assign.svg
[travis-url]: https://travis-ci.org/ljharb/object.assign
[dev-deps-svg]: https://david-dm.org/ljharb/object.assign/dev-status.svg?theme=shields.io
[dev-deps-url]: https://david-dm.org/ljharb/object.assign#info=devDependencies
[testling-png]: https://ci.testling.com/ljharb/object.assign.png
[testling-url]: https://ci.testling.com/ljharb/object.assign
[license-image]: http://img.shields.io/npm/l/object.assign.svg
[license-url]: LICENSE
-->
