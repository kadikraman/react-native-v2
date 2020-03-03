---
path: '/safe-area'
title: 'Safe Area'
order: 7
section: 'Basic components'
description: 'Using SafeAreaView to target to ensure the content is available'
---

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

How does it look? Not great I imagine. You might notice that the text is overlaid by the notification bar at the top of the screen. You could add some padding to the top of the screen, but that wouldn't serve for a general solution - while it might work for the phone you're testing on for the moment, there are tends of iPhones and hundreds of Android phones with different specs.

Thankfully there is something handy built into React Native to help with this. `SafeAreaView` is a component that automatically adds the necessary padding around your content to ensure that you don't overlap with the top and bottom of the screen. This is especially handy when iPhone X came out, as it handles the bottom spacing necessary for the notch.

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
