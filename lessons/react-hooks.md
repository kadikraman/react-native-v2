---
path: '/react-hooks'
title: 'useState, useCallback, useEffect'
order: 21
section: 'Hooks and Network Requests'
description: 'We talk about React Hooks and cover the main ones'
---

React hooks were added to React in v16.8.0 and React Native in v0.59. Hooks are a built in system for managing state and side-effects in function components. The introduction of hooks was incredibly exciting for the community. Before hooks the only way to do anything even mildly complicated like save component state or make a network request required a class component, or setting up redux and thunks or sagas. This is no longer the case! A lot of modern React and React Native applications are written using just function components and React hooks!

Hooks in React Native work _exactly_ the same as in plain React, so if you already know about hooks, you're good to go! Refer to the [React](https://reactjs.org/docs/hooks-intro.html) documentation on hooks for more info.

For the majority of use-cases, the only hooks you will need are `useState`, `useCallback` and `useEffect`. Let's look into these in detail.

## `useState`

[useState](https://reactjs.org/docs/hooks-state.html) is for saving and updating state inside the component.

```js
import React, { useState } from 'react';

const [value, setValue] = useState(0);
```

Hooks are placed _inside_ the component, as high as possible, always above the `return` statement. The `useState` hook returns an array of two items which you can name whatever you want: the first one is the current value of the item you're saving, and the second is a function that allows you to update the value.  Although you can choose any name you like for these functions, by convention they are named `varName` and `setVarName` as seen in `[value, setValue]`, `[colour, setColour]` etc. Following this convention improves your code readability by immediately signalling to yourself and other developers that this is a React `useState` hook so it is recommended to name accordingly unless you have a specific reason not to. Finally, the `0` we passed in is the initial value for our `value`. This is optional and will default to _undefined_.

In order to update this value, we simply call `setValue` with the new value. This will update `value` to reflect the new value, cause a re-render of the component and your UI will reflect the new state. 

There are two ways to update the value: 

1. Pass in a function which accepts the current value and returns the next value:

```js
setValue(currentValue => currentValue + 1);
```

2. Or set the value directly without any reference to the current value:

```js
setValue(1);
```

[🔍 useState example](https://snack.expo.io/@kadikraman/usestate-example)

## `useCallback`

[useCallback](https://reactjs.org/docs/hooks-reference.html#usecallback) is for any kind of action you may want to perform: be it a state update, a network request or launching a modal.

In our counter example before, we pass in the `onPress` function for incrementing and decrementing the counter directly. It's not so much of a problem, but it might get hard to read if the function was longer. So ideally we'd like to extract the `handleIncrement` and `handleDecrement` functions from the render method, like so:

```js
const handleIncrement = () => setCount(current => current + 1);
const handleDecrement = () => setCount(current => current - 1);

<TouchableOpacity onPress={handleIncrement}>

<TouchableOpacity onPress={handleDecrement}>

```

This works, but the problem is that the constants for `handleIncrement` and `handleDecrement` get re-initialized every time the component re-renders, and because React is built to be dynamic, this happens _a lot_. `useCallback` to the rescue!

```js
import React, { useCallback } from 'react';

const handleIncrement = useCallback(() => {
  setCount(current => current + 1);
}, []);
```

This may be a bit hard to read at first, but you'll soon get used to it. `useCallback` is a function that takes two arguments: the function we want to return (notice this is _exactly_ the function we had before), and an array of values that should trigger the function to be re-initialized. In our case, this array is empty, because the `useState` function is the same, and we're not using any other outside variables inside the `useCallback`. As a rule of thumb, any variables used inside the `useCallback` should be added to the array.

[🔍 useCallback example](https://snack.expo.io/@kadikraman/usecallback-example)

## `useEffect`

[useEffect](https://reactjs.org/docs/hooks-effect.html) is tied to the component render cycle. If you're already familiar with React Components, you can think of this as a combined `componentDidMount` and `componentDidUpdate`.

There are two main types of use-cases for `useEffect`: ones that require cleanup and ones that don't.

```js
useEffect(() => {
  ChatAPI.subscribeToFriendStatus(props.friend.id, status => setIsOnline(status.isOnline);

  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, []);
```

This bit of example code shows how you might subscribe to a chat API. Notice that the function body does the subscription, and the return value is a function that removes the subscription. Any function you return from a `useEffect` will be run when the component is unmounted. This is important to keep in mind to prevent memory leaks.

The other use-case is similar to the above, but for actions that do not require cleanup.

```js
useEffect(() => {
  someActionWeNeedToDoOnce();
}, []);
```

The above code will only be executed once when the component is rendered and never again.

Note that the second argument to `useEffect` is an array of items that should trigger the effect to run again (the same as the second argument for `useCallback`). The second argument is optional, but if it is not provided it will run on every component render. If you want to run the effect only on component load (equivalent to `componentDidMount` in a React class component), provide an empty array `[]`. You should be especially careful about making sure you pass in the empty array when making network requests that trigger a component re-render otherwise you'll end up in an infinite loop!

[🔍 useEffect example](https://snack.expo.io/@kadikraman/useeffect-example)

☝️ you should run this on your phone or the in-browser emulator or you'll get CORS errors. In this example we do a network request to fetch some random cat facts when the component is rendered.

