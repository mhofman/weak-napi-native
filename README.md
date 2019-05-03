# @mhofman/weak-napi-native

### Native bindings of the `weak-napi` package

Exports the native bindings used internally by the [`weak-napi`](https://npmjs.org/package/weak-napi) package.

# ObjectInfo

```javascript
const { ObjectInfo } = require("@mhofman/weak-napi-native");
// or
const ObjectInfo = require("@mhofman/weak-napi-native/object-info");

let obj = {};

// The callback is currently mandatory even if not using
let info = new ObjectInfo(obj, () => {});

console.log(info.target === obj);

obj = undefined;

setImmediate(() => {
  gc();

  console.log(info.target === undefined);
});
```

# WeakTag

```javascript
const { ObjectInfo, WeakTag } = require("@mhofman/weak-napi-native");
// or
const ObjectInfo = require("@mhofman/weak-napi-native/object-info");
const WeakTag = require("@mhofman/weak-napi-native/weak-tag");

const weakMap = new WeakMap();

let obj = {};

let info = new ObjectInfo(obj, () => {
  console.log("obj was collected");
});

// There should only be one `WeakTag` per `ObjectInfo`
weakMap.set(obj, new WeakTag(info));

obj = undefined;

setImmediate(gc);
```
