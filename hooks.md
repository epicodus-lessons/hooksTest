# React useState Hook

In early 2019, React released version 16.8 which included the much-anticipated introduction of hooks. Hooks were developed as a solution to a problem programmers had been dealing with since the outset of React: how to use state in a functional component without having to completely refactor it into a class component?

This short lesson will introduce you to the React useState hook by walking through a very simple counter app. Our app will include a button which increases the value of a counter, a button to show and hide, and a display of the counter's value. Let's jump right in.

The first thing we need to do is add _{ useState }_ to our import statement at the top of the document. We'll also set up a basic functional component.

```javascript
import React, { useState } from 'react';

function SomeComponent() {
  return(
    <div>
    </div>
  )
}

export default SomeComponent;
```

Now we're ready to implement the useState object, which always returns an array containing two items. The first item is the state property and the second is a method we can use to set the property's value. _useState_ itself takes an argument, which will set the state property's initial value. We can initialize this with a number, a boolean, a string, or an object. Let's initialize ours with the number 0.


```javascript
...

function SomeComponent() {

  const [counter, setCounter] = useState(0);

  return(
    <div>
    </div>
  )
}

...
```
Now we're ready to use the state property and the setState method in our JSX. We can simply call upon _counter_, which will display its current value. To use the method, we can create an onClick listener in a button and set its value equal to a function implicitly returning the _setCounter_ method. We need this to be a callback function so we can pass in an argument, otherwise it'll run on page load. This will replace the current value of _counter_ (note: this will completely overwrite its previous value).

```javascript
...

function SomeComponent() {

  const [counter, setCounter] = useState(0);

  return (
    <div>
      <h1>{counter}</h1>
      <button onClick={() => setCounter(counter + 1)}>Count!</button>
    </div>
  );
}

...
```

Pretty straightforward, isn't it? With just a couple of lines, we have local state in a function component. Remember, this has nothing to do with our single-source-of-truth global state, but it's still quite handy.

Let's say we want to add another property to our local state object. We *could* approach that like so:

```javascript

...
function SomeComponent() {

  const [bundle, setBundle] = useState({"hidden": true, "counter": 0});

  return (
    <div>
      {hidden ? <h1>{counter}</h1> : <h1>Count Hidden</h1>}

      <button onClick={() => setHidden({"hidden": hidden, "counter": bundle.counter +1})}>Count!</button>
      <button onClick={() => setBundle({...bundle, "hidden": !bundle.hidden})}>Hide/Show</button>
    </div>
  );
}

...
```

React's _useState()_ accepts any data type as an argument, including objects. We could create as many properties as we like and call on them using dot notation. But while the above approach works, it is not recommended. The React documentation instead recommends creating multiple instances of useState and calling on them as separate variables. Take a look at this approach:  


```javascript

...
function SomeComponent() {

  const [counter, setCounter] = useState(0);
  const [hidden, setHidden] = useState(true);

  return (
    <div>
      {hidden ? <h1>{counter}</h1> : <h1>Count Hidden</h1>}
      <button onClick={() => setCounter(counter + 1)}>Count!</button>
      <button onClick={() => setHidden(!hidden)}>Hide/Show</button>
    </div>
  );
}

...
```

It's not only easier to read the state variable declarations, it's easier to use the state in our JSX.

The useState hook is very useful and pretty simple to understand and implement. If you'd like to learn more about the useState hook, take a look at the official [React Hooks Docs](https://reactjs.org/docs/hooks-intro.html).
