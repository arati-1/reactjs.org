---
title: defaultChecked
---

<Intro>

The `defaultChecked` attribute is supported by the `<input>` components of type `checkbox` or `radio button`. You can use it set whether the component is checked when it is first mounted.

`defaultChecked` is the uncontrolled equivalent of the [`checked`](/apis/checked) attribute.

</Intro>

- [Usage](#usage)
  - [Using the `defaultChecked` attribute](#using-the-defaultChecked-attribute)

## Usage {/*usage*/}

### Using the `defaultChecked` attribute {/*using-the-defaultChecked-attribute*/}

In this example, an `<input>` of the type `checkbox` is being rendered. We set the `defaultChecked` attribute to `true` using the [`useState`](/apis/usestate) hook. Hence, the checkbox is checked when the component loads.

<Sandpack>

``` js

import { useState } from 'react';

export default function Checkbox() {
  const [checked, setChecked] = useState(true);

  return (
    <label>
      <input type="checkbox"
        defaultChecked={checked}
        onChange={() => setChecked(!checked)}
      />
      Select
    </label>
  );
}

```
</Sandpack>
