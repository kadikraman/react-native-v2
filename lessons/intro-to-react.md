---
path: '/intro-to-react'
title: 'Basic React Native components'
order: 5
section: 'Basic components'
description: 'We get started with the basic building blocks of a React Native application'
---

If you're already familiar with React then you've got a head start, lucky you! Before we dive into React Native, let's start by looking at this "hello world" React component:

```js
// App.js

import React from 'react';

const App = () => {
  return <div>Hello, world!</div>;
};

export default App;
```

This is a minimal React component. If you're used React before, this will be familiar to you. If not, let's talk through what's going on here.

React uses what they call JSX as syntax sugar for displaying components. JSX stands for "JavaScript and XML", and although XML is quite dated, it really works out for React, because the XML syntax looks very similar to HTML! The bonus is that we can do JavaScript around it.

At the top of the file we have an import statement - `import React from 'react';` - though `React` is not used in the file. This is because `React` is needed for the JSX. As a rule of thumb, if the file includes any components with braces (`<>`) you'll need to import React.

Now let's look at a corresponding React Native component:

```js
// App.js

import React from 'react';
import { View, Text } from 'react-native';

const App = () => {
  return (
    <View>
      <Text>Hello, world!</Text>
    </View>
  );
};

export default App;
```

There are a couple of important differences here. We can't use `div`, `span`, `p` or other html elements in React Native. Instead, we have special native components. The notable difference is that you have to import these components from `react-native` rather than just having them built into jsx.

- `<View>` - if you're already familiar with web development, you can think of `<View>` as a native equivalent to `<div>`. It's a container to use for styling and positioning the elements within.

- `<Text>` - the `<Text>` component is used for displaying, you guessed it, text! In React Native, all text you want to display _must_ be contained in `<Text>` tags or you'll have errors.

React in the web has a root component that binds to a single node in the DOM. React Native works differently, but suffice it to say that the app entry point is the `App.js` in the root directory.
