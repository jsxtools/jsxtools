# babel-preset-smooth-react [<img src="https://avatars.githubusercontent.com/u/52989093" alt="" width="90" height="90" align="right">][toolchain]

[<img alt="npm version" src="https://img.shields.io/npm/v/babel-preset-smooth-react.svg" height="20">](https://www.npmjs.com/package/babel-preset-smooth-react)
[<img alt="build status" src="https://img.shields.io/travis/jsxtools/toolchain/master.svg" height="20">](https://travis-ci.org/jsxtools/toolchain)
[<img alt="issue tracker" src="https://img.shields.io/github/issues/jsxtools/toolchain/babel-preset-smooth-react.svg" height="20">](https://github.com/jsxtools/toolchain/issues?q=is:issue+is:open+label:babel-preset-smooth-react)
[<img alt="pull requests" src="https://img.shields.io/github/issues-pr/jsxtools/toolchain/babel-preset-smooth-react.svg" height="20">](https://github.com/jsxtools/toolchain/pulls?q=is:pr+is:open+label:babel-preset-smooth-react)

[babel-preset-smooth-react] is a Babel preset for smooth React projects.

It is a light wrapper around [babel-preset-react] that allows you to:

- Write JSX in JavaScript without adding `react` imports.
- Write `class` and `for` attributes in JSX elements.
- Import modules from `paths` specified in `jsconfig.json`.

## Installation

Add **babel-preset-smooth-react** to your project:

```sh
npm install babel-preset-smooth-react --save-dev
```

## Usage

Add **babel-preset-smooth-react** to your babel configuration:

```js
// babel.config.js
{
  "presets": ["smooth-react"]
}
```

Define **path mapping** in `tsconfig.json` or `jsconfig.json`:

```js
// tsconfig.json or jsconfig.json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "@com/*": ["components/*"],
      "@css/*": ["components/*.module.css"]
    }
  }
}
```

Enjoy writing smooth **React**:

```js
// App.js (before)
import Button from '@com/Button';
import style from '@css/Button/style';

export const App = props => <Button class={style.Button}>{props.children}</Button>;
```

```js
// App.js (after)
import { createElement } from 'react';
import Button from '/path/to/src/components/Button';
import ButtonStyle from '/path/to/src/components/style.module.css';

export const App = props => createElement(Button, { className: style.Button }, props.children);
```

## Options

All options are passed through into [babel-preset-react], with additional
options provided to other plugins.

### pragma

The `pragma` option defines how the element creation function is added.

```js
// transforms <foo /> into createElement('foo') and potentially imports React (default)
{
  pragma: '{ createElement } from react'
}
```

```js
// transforms <foo /> into h('foo') and potentially imports Preact
{
  pragma: '{ h } from preact'
}
```

### pragmaFrag

The `pragmaFrag` option defines how the fragment creation function is added.

```js
// transforms <></> into Fragment and potentially imports React (default)
{
  pragmaFrag: '{ Fragment } from react'
}
```

```js
// transforms <></> into Fragment and potentially imports Preact
{
  pragmaFrag: '{ Fragment } from preact'
}
```

### throwIfNamespace

The `throwIfNamespace` option toggles whether or not to throw an error if a XML
namespaced tag name is used. For example:

```jsx
// will not throw (default)
<f:image />
```

### development

The `development` option toggles plugins that aid in development, such as
[@babel/plugin-transform-react-jsx-self] and
[@babel/plugin-transform-react-jsx-source].

### useBuiltIns

The `useBuiltIns` option determines whether the preset should use native
built-ins instead of trying to polyfill behavior for any plugins requiring it.

[babel-preset-react]: https://babeljs.io/docs/en/next/babel-preset-react.html
[babel-preset-smooth-react]: https://github.com/jsxtools/toolchain/tree/master/packages/babel-preset-smooth-react
[toolchain]: https://github.com/jsxtools/toolchain
