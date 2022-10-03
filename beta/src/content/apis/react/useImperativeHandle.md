---
title: useImperativeHandle
---

<Intro>

`useImperativeHandle` customizes the value that is exposed to the parent components when using `ref`.

```js
useImperativeHandle(ref, createHandle, [deps])
```
</Intro>

<InlineToc />

## Usage {/*usage*/}

### Modifying the `ref` of a parent component by a child component {/*modifying-the-ref-of-a-parent-component-by-a-child-component*/}

Add `useImperativeHandle` to customize the value the parent component receives when it tries to get a `ref` from a child component. To use this Hook, you must first opt into exposing the ref, which you can do with [`forwardRef`](/apis/react/forwardRef).

For example, here the `MyInput` component exposes an object with a single `focus` method:

```js {5-9}
const MyInput = forwardRef((props, ref) => {
  const inputRef = useRef(null);
  const { label, ...otherProps } = props;

  useImperativeHandle(ref, () => ({
    focus() {
      inputRef.current.focus();
    }
  }))

  return (
    <label>
      {label}
      <input {...otherProps} ref={inputRef} />
    </label>
  );
});
```

Instead of exposing an entire DOM node, you can expose a custom object, called an *imperative handle*, with a more constrained set of methods. To do this, you'd need to define a separate ref to hold the DOM node.

As a result, the parent component can call `focus()` on `MyInput` but will not have access to the underlying `<input>` DOM node.

```js {5,10}
function Form() {
  const ref = useRef(null);

  function handleClick() {
    ref.current.focus();
  }

  return (
    <>
      <MyInput ref={ref} />
      <button onClick={handleClick}>Focus</button>
    </>
  )
}
```

The object inside of `inputRef.current` is the object that was returned from the function.

You won't use this technique very often. Still, it's helpful if you want to expose some imperative methods like focusing, scrolling, or triggering animations to the parent component without giving the parent full access to the underlying DOM node.

<Sandpack>

```js
import React, {useImperativeHandle, useRef ,forwardRef} from "react";

const MyInput = forwardRef((props, ref) => {
  const inputRef = useRef(null);
  const { label, ...otherProps } = props;

  useImperativeHandle(ref, () => ({
    focus() {
      inputRef.current.focus();
    }
  }))

  return (
    <label>
      {label}
      <input {...otherProps} ref={inputRef} />
    </label>
  );
});

export default function Form() {
  const ref = useRef(null);

  function handleClick() {
    ref.current.focus();
  }

  return (
    <>
      <MyInput ref={ref} />
      <button onClick={handleClick}>Focus</button>
    </>
  )
}

```
</Sandpack>

## Reference {/*reference*/}

### `useImperativeHandle(ref, createHandle, [deps])` {/*useimperativehandleref-createhandle-deps*/}

Call `useImperativeHandle` outside any component to use it.

```js
import { useImperativeHandle } from 'react';

useImperativeHandle(ref, createHandle, [deps])
```
#### Parameters {/*parameters*/}
* `ref`: `useImperativeHandle` accepts a `ref` passed by the parent component as a parameter.

* `createHandle`: A handler function whose return value replaces the stored value in the `ref` object, and the whole function is updated when the dependency list changes. On subsequent renders, React will return the same `ref` again if the `dependencies` have not changed since the last render.

* `dependencies`: The list of all reactive values referenced inside of the `createHandle` code to determine when the `ref` value inside gets updated. If one of the dependencies changes, then the `ref` value is updated.

#### Returns {/*returns*/}

`useImperativeHandle` returns a custom function or in-built function of the child component. This return value modifies the `ref` object passed by the parent component.
