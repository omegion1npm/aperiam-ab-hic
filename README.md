# @omegion1npm/aperiam-ab-hic

[![npm version](https://img.shields.io/npm/v/@omegion1npm/aperiam-ab-hic.svg)](https://www.npmjs.com/package/@omegion1npm/aperiam-ab-hic)
[![Downloads/month](https://img.shields.io/npm/dm/@omegion1npm/aperiam-ab-hic.svg)](http://www.npmtrends.com/@omegion1npm/aperiam-ab-hic)
[![Build Status](https://github.com/omegion1npm/aperiam-ab-hic/workflows/CI/badge.svg)](https://github.com/omegion1npm/aperiam-ab-hic/actions)

Constants and utilities about visitor keys to traverse AST.

## 💿 Installation

Use [npm] to install.

```bash
$ npm install @omegion1npm/aperiam-ab-hic
```

### Requirements

- [Node.js] `^18.18.0`, `^20.9.0`, or `>=21.1.0`


## 📖 Usage

To use in an ESM file:

```js
import * as evk from "@omegion1npm/aperiam-ab-hic"
```

To use in a CommonJS file:

```js
const evk = require("@omegion1npm/aperiam-ab-hic")
```

### evk.KEYS

> type: `{ [type: string]: string[] | undefined }`

Visitor keys. This keys are frozen.

This is an object. Keys are the type of [ESTree] nodes. Their values are an array of property names which have child nodes.

For example:

```
console.log(evk.KEYS.AssignmentExpression) // → ["left", "right"]
```

### evk.getKeys(node)

> type: `(node: object) => string[]`

Get the visitor keys of a given AST node.

This is similar to `Object.keys(node)` of ES Standard, but some keys are excluded: `parent`, `leadingComments`, `trailingComments`, and names which start with `_`.

This will be used to traverse unknown nodes.

For example:

```js
const node = {
    type: "AssignmentExpression",
    left: { type: "Identifier", name: "foo" },
    right: { type: "Literal", value: 0 }
}
console.log(evk.getKeys(node)) // → ["type", "left", "right"]
```

### evk.unionWith(additionalKeys)

> type: `(additionalKeys: object) => { [type: string]: string[] | undefined }`

Make the union set with `evk.KEYS` and the given keys.

- The order of keys is, `additionalKeys` is at first, then `evk.KEYS` is concatenated after that.
- It removes duplicated keys as keeping the first one.

For example:

```js
console.log(evk.unionWith({
    MethodDefinition: ["decorators"]
})) // → { ..., MethodDefinition: ["decorators", "key", "value"], ... }
```

## 📰 Change log

See [GitHub releases](https://github.com/omegion1npm/aperiam-ab-hic/releases).

## 🍻 Contributing

Welcome. See [ESLint contribution guidelines](https://eslint.org/docs/developer-guide/contributing/).

### Development commands

- `npm test` runs tests and measures code coverage.
- `npm run lint` checks source codes with ESLint.
- `npm run test:open-coverage` opens the code coverage report of the previous test with your default browser.


[npm]: https://www.npmjs.com/
[Node.js]: https://nodejs.org/
[ESTree]: https://github.com/estree/estree
