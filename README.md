# ECMAScript Proposal: `Performant object property counting`

## Status

Champion: Ruben Bridgewater, Jordan Harband

Author: Ruben Bridgewater <ruben@bridgewater.de>, Jordan Harband <ljharb@gmail.com>

Stage: 1

## Overview

This proposal introduces three built-in methods that efficiently obtain the count of an object's own properties without the performance overhead of intermediate array allocations:

- `Object.keysLength(target)` — counts own enumerable string-keyed properties (including array indices), mirroring `Object.keys`.
- `Object.getOwnPropertyNamesLength(target)` — counts all own string-keyed properties, mirroring `Object.getOwnPropertyNames`.
- `Object.getOwnPropertySymbolsLength(target)` — counts all own symbol-keyed properties, mirroring `Object.getOwnPropertySymbols`.

## Motivation

Developers frequently rely on patterns like:

```js
const obj = { a: 1, b: 2 };
const count = Object.keys(obj).length;
```

However, this approach creates unnecessary memory overhead and garbage collection pressure, as an intermediate array is allocated solely for counting properties. Highly-used runtimes, frameworks, and libraries (e.g., Node.js, React, Lodash, Angular, Storybook, Excalidraw, VS Code, Svelte, Next.js, three.js, Puppeteer, Tailwind, ...) frequently utilize `Object.keys(obj).length`, compounding performance issues across applications.

For instance, React often counts props or state keys:

```js
// React component example
const propCount = Object.keys(this.props).length;
```

Replacing these patterns with a native and optimized counting method significantly reduces memory overhead, garbage collection, and as such, runtime performance impacts.

### [Concrete usage examples](./examples.md)

## Problem Statement

Currently, accurately counting object properties involves verbose and inefficient workarounds:

```js
const count = [
  ...Object.getOwnPropertyNames(obj),
  ...Object.getOwnPropertySymbols(obj)
].length;

const reflectCount = Reflect.ownKeys(obj).length;

assert.strictEqual(count, reflectCount);
```

This creates intermediate arrays, causing unnecessary memory usage and garbage collection, impacting application performance — especially at scale and in performance-critical code paths.

These APIs eliminate intermediate arrays for common counting patterns and align directly with the semantics of their existing counterparts.

## Decomposition Plan: Three Independent APIs

To facilitate incremental, independently-approvable progress and to align closely with existing, well-understood APIs, this proposal will be rewritten as three focused methods that are drop-in, non-allocating equivalents of existing patterns:

- `Object.keysLength(target)` ≈ `Object.keys(target).length` (no intermediate array)
- `Object.getOwnPropertyNamesLength(target)` ≈ `Object.getOwnPropertyNames(target).length` (no intermediate array)
- `Object.getOwnPropertySymbolsLength(target)` ≈ `Object.getOwnPropertySymbols(target).length` (no intermediate array)

Each API is specified below in a separate section using the current structure (Overview, Proposed API, Semantics, Examples, Polyfill), so they can advance through the process independently.

## Object.keysLength

### Overview

`Object.keysLength` returns the number of an object's own enumerable string-keyed properties (including array index properties), without allocating the array produced by `Object.keys`.

### Proposed API

```js
Object.keysLength(target)
```

### Explicit Semantics

- Throws `TypeError` if `target` is not an object.
- Counts only own properties.
- Counts only enumerable properties.
- Counts only string-keyed properties (including array indices).
- Does not allocate any intermediate arrays.

### Examples

```js
Object.keysLength({}); // 0
Object.keysLength({ a: 1, b: 2 }); // 2
Object.keysLength(Object.create({ a: 1 })); // 0 (own only)
Object.keysLength(Object.defineProperty({}, 'x', { value: 1, enumerable: false })); // 0
```

### Polyfill (for reference)

```js
Object.keysLength = function keysLength(target) {
  if (typeof target !== 'object' || target === null) {
    throw new TypeError('Expected an object');
  }
  return Object.keys(target).length;
};
```

## Object.getOwnPropertyNamesLength

### Overview

`Object.getOwnPropertyNamesLength` returns the number of an object's own string-keyed properties, regardless of enumerability, without allocating the array produced by `Object.getOwnPropertyNames`.

### Proposed API

```js
Object.getOwnPropertyNamesLength(target)
```

### Explicit Semantics

- Throws `TypeError` if `target` is not an object.
- Counts only own properties.
- Counts only string-keyed properties (including array indices).
- Counts both enumerable and non-enumerable properties.
- Does not allocate any intermediate arrays.

### Examples

```js
Object.getOwnPropertyNamesLength({}); // 0
Object.getOwnPropertyNamesLength({ a: 1, b: 2 }); // 2
const o = Object.defineProperty({}, 'x', { value: 1, enumerable: false });
Object.getOwnPropertyNamesLength(o); // 1
```

### Polyfill (for reference)

```js
Object.getOwnPropertyNamesLength = function getOwnPropertyNamesLength(target) {
  if (typeof target !== 'object' || target === null) {
    throw new TypeError('Expected an object');
  }
  return Object.getOwnPropertyNames(target).length;
};
```

## Object.getOwnPropertySymbolsLength

### Overview

`Object.getOwnPropertySymbolsLength` returns the number of an object's own symbol-keyed properties, without allocating the array produced by `Object.getOwnPropertySymbols`.

### Proposed API

```js
Object.getOwnPropertySymbolsLength(target)
```

### Explicit Semantics

- Throws `TypeError` if `target` is not an object.
- Counts only own properties.
- Counts only symbol-keyed properties.
- Counts properties regardless of enumerability (aligned with `Object.getOwnPropertySymbols`).
- Does not allocate any intermediate arrays.

### Examples

```js
Object.getOwnPropertySymbolsLength({}); // 0
const s = Symbol('s');
const o = { [s]: 1 };
Object.getOwnPropertySymbolsLength(o); // 1
```

### Polyfill (for reference)

```js
Object.getOwnPropertySymbolsLength = function getOwnPropertySymbolsLength(target) {
  if (typeof target !== 'object' || target === null) {
    throw new TypeError('Expected an object');
  }
  return Object.getOwnPropertySymbols(target).length;
};
```

## Detailed Examples and Edge Cases

- **Empty object**:

```js
Object.keysLength({}); // 0
Object.getOwnPropertyNamesLength({}); // 0
Object.getOwnPropertySymbolsLength({}); // 0
```

- **Object without prototype**:

```js
const obj = Object.create(null);
obj.property = 1;
Object.keysLength(obj); // 1 (if enumerable)
Object.getOwnPropertyNamesLength(obj); // 1
```

```js
const obj2 = { __proto__: null };
obj2.property = 1;
Object.keysLength(obj2); // 1 (if enumerable)
Object.getOwnPropertyNamesLength(obj2); // 1
```

- **Array index keys**:

See https://tc39.es/ecma262/#array-index

```js
let obj = { "01": "string key", 1: "index", 2: "index" };
Object.keysLength(obj); // 3

obj = { "0": "index", "-1": "string key", "01": "string key" };
Object.keysLength(obj); // 3
```

- **String based keys**:

```js
const obj = { "01": "string key", 1: "index", 2: "index" };
Object.keysLength(obj); // 3
Object.getOwnPropertyNamesLength(obj); // 3 (or more if non-enumerable props exist)
```

- **Symbol based keys**:

```js
const obj = { [Symbol()]: "symbol", 1: "index", 2: "index" };
Object.getOwnPropertySymbolsLength(obj); // 1
```

## Explicit Semantics

- Only own properties are considered.
- Enumerability semantics align with the corresponding existing APIs:
  - `Object.keysLength`: counts only enumerable string-keyed properties (including array indices).
  - `Object.getOwnPropertyNamesLength`: counts all string-keyed properties, regardless of enumerability.
  - `Object.getOwnPropertySymbolsLength`: counts all symbol-keyed properties, regardless of enumerability.
- Implementations must avoid intermediate array allocations entirely.

## Algorithmic Specification

The native implementation should strictly avoid creating intermediate arrays or unnecessary allocations. For each method:

1. Initialize `count` to `0`.
2. Iterate directly over the object's own property keys via its internal slots, without materializing arrays.
3. For each own property key:
   - For `Object.keysLength`: if the key is a string and the property is enumerable, increment `count`.
   - For `Object.getOwnPropertyNamesLength`: if the key is a string (enumerable or not), increment `count`.
   - For `Object.getOwnPropertySymbolsLength`: if the key is a symbol (enumerable or not), increment `count`.
4. Return `count`.

See the [spec proposal](./spec.emu) for details.

## Alternatives Considered

- **Chosen approach: Multiple separate methods**: This document pursues three focused methods (`Object.keysLength`, `Object.getOwnPropertyNamesLength`, `Object.getOwnPropertySymbolsLength`) to minimize option surfaces, align with existing API shapes, and enable independent advancement and evaluation.
- **Single method with options bag (`Object.propertyCount(target, options)`)**: Previously considered and rejected. While flexible, it:
  - Produces subtle combinatorial semantics (e.g., enumerability + key type).
  - Diverges from established precedent of focused, orthogonal methods (`keys`, `getOwnPropertyNames`, `getOwnPropertySymbols`).
- **Using booleans for key types (within an options bag)**: Rejected as part of the single-method approach due to confusing defaults and mismatched state space.

## TC39 Stages and Champion

- Ready for **Stage 2**

## Use Cases

- Improved readability and explicit intent
- Significant **performance** gains
- **Reduced memory** overhead
- **Simpler code**

## Precedent

Frequent patterns in widely-used JavaScript runtimes, frameworks, and libraries (Node.js, React, Angular, Lodash) demonstrate the common need for an optimized property counting mechanism.

The regular expression exec/match/matchAll methods produce a "match object" that is an Array, with non-index string properties on it (lastIndex, groups, etc).

## Considerations

- **Backwards compatibility**: Fully backward compatible.
- **Performance**: Native implementation will significantly outperform existing approaches by eliminating intermediate arrays.
- **Flexibility**: Clear, focused methods cover the common cases without configuration complexity.
- **Simplicity**: Improved code readability and clarity.
- **Future proofing**: Additional focused APIs can be added as needed (e.g., enumerable symbol discovery and counting) without overloading a single method with options.

## Future Additions

The following additions are plausible follow-ups that align with existing method families and the decomposition above:

- `Object.symbols(target)`: A new method analogous to `Object.keys(target)` that returns an array of an object's own enumerable symbol-keyed properties, in insertion order. This fills the current gap between `Object.keys` (enumerable string keys) and `Object.getOwnPropertySymbols` (all own symbols regardless of enumerability).
- `Object.symbolsLength(target)`: A non-allocating counterpart to `Object.symbols(target).length`, analogous to `Object.keysLength`. This would be specified identically to `Object.keysLength`, but limited to enumerable symbol-keyed properties.

These can be advanced together independently of the three methods above and would provide a complete, parallel set of primitives for both string and symbol keys: discovery (`keys`/`symbols`) and counting (`keysLength`/`symbolsLength`), as well as total string/symbol counts via `getOwnPropertyNamesLength` and `getOwnPropertySymbolsLength`.

## Conclusion

`Object.keysLength`, `Object.getOwnPropertyNamesLength`, and `Object.getOwnPropertySymbolsLength` offer substantial performance benefits by efficiently counting object properties without intermediate arrays, enhancing ECMAScript with clarity, performance, and reduced memory overhead while aligning with well-understood existing APIs.
