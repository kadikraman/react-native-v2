---
path: '/intro-to-react'
title: 'Basic React Native components'
order: 7
section: 'Basic components'
description: 'Quick intro to React and the basic building blocks of React Native: View, Text and ScrollView'
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

- `<ScrollView>` - pages do not scroll by default. If you have lots of content to display, you can use a `ScrollView`

- `<Text>` - the `<Text>` component is used for displaying, you guessed it, text! In React Native, all text you want to display _must_ be contained in `<Text>` tags or you'll have errors.

Now that we've got some components to work with - let's get coding!

## Basic Components and SafeAreaView

Open your `App.js`, delete the content and replace it with our "Hello, World" template.

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

How does it look? Not great I imagine. You might notice that the text is overlaid by the notification bar at the top of the screen. You could add some padding to the top of the screen, but that wouldn't serve for a general solution - while it might work for the phone you're testing on for the moment, there are tens of iPhones and hundreds of Android phones with different specs.

Thankfully there is something handy built into React Native to help with this. `SafeAreaView` is a component that automatically adds the necessary padding around your content to ensure that you don't overlap with the top and bottom of the screen. This was especially handy when iPhone X came out, as it handles the bottom spacing necessary for the notch.

All you need to do is to import the `SafeAreaView` from `react-native` and wrap your content around it like so:

```js
// App.js

import React from 'react';
import { View, Text, SafeAreaView } from 'react-native';

const App = () => {
  return (
    <SafeAreaView>
      <View>
        <Text>Hello, world!</Text>
      </View>
    </SafeAreaView>
  );
};

export default App;
```

Great! Now you can be confident your content will be visible regardless of the device.

[🔗 Expo 49584b83f6871b73bd3fc6219db048e0875e8f53](https://github.com/kadikraman/AwesomeProjectExpo/commit/49584b83f6871b73bd3fc6219db048e0875e8f53)

[🔗 RN 43e1c4d6ae62f4befb51857fa4b95b1c14ddd3de](https://github.com/kadikraman/AwesomeProjectRN/commit/43e1c4d6ae62f4befb51857fa4b95b1c14ddd3de)
