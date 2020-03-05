---
path: '/modals'
title: 'Opening a full screen modal'
order: 22
section: 'Forms'
description: 'Opening a full screen modal'
---

For the forms challenge, we'd like to be start adding our own color schemes to the list. But the best way to do that would be using a modal, so first we need to update out navigation so allow us to trigger display modals. In order to do this, we'll have to once again refactor our navigation.

Looking at our navigation as a tree, this is the layout we need to get to:

<div style="display:flex; flex-direction:row">
    <div style="width:500px;margin:0 auto;margin-bottom:20px">
        <img alt="Style challenge iOS" src="./images/stack.png" />
    </div>
</div>

Source: react navigation [docs](https://reactnavigation.org/docs/modal/)

Our current layout only has the RootStack, HomeScreen, and DetailsScreen, so we need to add the a MainStack and a Modal Screen in the middle.

First lets rename our Stack to RootStack:

```js
const RootStack = createStackNavigator();
```

Now let's add the MainStack and pull our existing navigation all out of the App component and into it's own MainStackScreen component:

```js
const MainStackScreen = () => {
  return (
    <MainStack.Navigator>
      <MainStack.Screen name="Home" component={Home} />
      <MainStack.Screen
        name="ColorPalette"
        component={ColorPalette}
        options={({ route }) => ({ title: route.params.paletteName })}
      />
    </MainStack.Navigator>
  );
};
```

Finally, update the App component to use RootStack and MainStackScreen

```js
const App = () => {
  return (
    <NavigationContainer>
      <RootStack.Navigator mode="modal">
        <RootStack.Screen
          name="Main"
          component={MainStackScreen}
          options={{ headerShown: false }}
        />
      </RootStack.Navigator>
    </NavigationContainer>
  );
};
```

Note that we had to use `mode="modal"` on `RootStack.Navigator` to tell the navigation that we're going to have a modal in there. We also had to add `options={{ headerShown: false }}` to `RootStack.Screen`. If we didn't do this, we'd end up with two top navs in our main stack!

[🔗 RN 3d4cd0f](https://github.com/kadikraman/AwesomeProjectRN/commit/3d4cd0f96e38a74e1ebaebd3285a538774b71458)

Now all we need to do is add the modal. Create a new file called `ColorPaletteModal.js` in your `screens` directory and add some default content:

```js
// screens/AddNewPaletteModal.js

import React from 'react';
import { View, Text } from 'react-native';

const AddNewPaletteModal = () => {
  return (
    <View>
      <Text>Hello, world!</Text>
    </View>
  );
};

export default AddNewPaletteModal;
```

[🔗 RN b9dea0f](https://github.com/kadikraman/AwesomeProjectRN/commit/b9dea0fe779518c7cd8d11c1d52282c922e7c3f0)
