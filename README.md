# use-immer

A hook to use [immer](https://github.com/mweststrate/immer) as a React [hook](https://reactjs.org/docs/hooks-intro.html) to manipulate state.

_Warning: Hooks are currently a React [RFC](https://github.com/reactjs/rfcs/pull/68) and **not ready for production**. Use at minimum `react@16.7.0-alpha.0` to use this package._

# Installation

`npm install use-immer`

# API

`useImmer(initialState)` is very similar to [`useState`](https://reactjs.org/docs/hooks-state.html).
The function returns a tuple, the first value of the tuple is the current state, the second is the updater function,
which accepts an [immer producer function](https://github.com/mweststrate/immer#api), in which the `draft` can be mutated freely, until the producer ends and and the changes will be made immutable and become the next state.

# Example

Example ([try it online](https://codesandbox.io/s/l97yrzw8ol)):

```javascript
import React from "react";
import { useImmer } from "use-immer";


function App() {
  const [person, updatePerson] = useImmer({
    name: "Michel",
    age: 33
  });

  function updateName(name) {
    updatePerson(draft => {
      draft.name = name;
    });
  }

  function becomeOlder() {
    updatePerson(draft => {
      draft.age++;
    });
  }

  return (
    <div className="App">
      <h1>
        Hello {person.name} ({person.age})
      </h1>
      <input
        onChange={e => {
          updateName(e.target.value);
        }}
        value={person.name}
      />
      <br />
      <button onClick={becomeOlder}>Older</button>
    </div>
  );
}
```

(obviously, immer is a little overkill for this example)