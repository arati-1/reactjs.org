---
title: defaultValue
---

<Intro>

The `defaultValue` attribute is supported by the `<input>`, `<select>`, and `<textarea>` components. You can use it to set the value of the component when it is first mounted.

`defaultValue` is the uncontrolled equivalent of the [`value`](/apis/value) attribute.

</Intro>

- [Usage](#usage)
  - [Using the `defaultValue` attribute](#using-the-defaultValue-attribute)

## Usage {/*usage*/}

### Using the `defaultValue` attribute {/*using-the-defaultValue-attribute*/}

In this example, `MyComponent` is rendering a `<textarea>` component with the `defaultValue` set. Hence, the `<textarea>` has default text when the component mounts.

<Sandpack>

``` js App.js

import React from 'react';
import { useState } from 'react';

export default function MyComponent() {
  const [value, setValue] = useState("First name");

    return (
      <>
        <h3>Input</h3>
        <label htmlFor="content">
          Enter Name
        </label>
        <textarea
          id="content"
          defaultValue={value}
        />
      </>
    );
  }

```
</Sandpack>
