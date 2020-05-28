---
path: '/modals'
title: 'Opening a full screen modal'
order: 26
section: 'Forms'
description: 'Opening a full screen modal'
---

Before we get stuck into our form challenge, we'll need to do some prep work. Specifically, we need to open a modal to put that form in. This requires some tinkering with navigation again, so we'll dp that first. This is an illustration of what we'd like to get to:

<div style="width:800px; display:flex; margin:0 auto;">
  <img alt="Open modal demo" src="./images/open-modal-demo.gif" width="800" />
</div>

For the forms challenge, we'd like to be start adding our own color schemes to the list. But the best way to do that would be using a modal, so first we need to update out navigation so allow us to trigger display modals. In order to do this, we'll have to once again refactor our navigation.

Looking at our navigation as a tree, this is the layout we need to get to:

<div style="width:500px;margin:0 auto;margin-bottom:20px">
    <img alt="Navigation stack" src="./images/stack.png" />
</div>

Source: react navigation [docs](https://reactnavigation.org/docs/modal/)

Our current layout only has the RootStack, HomeScreen, and DetailsScreen, so we need to add the a MainStack and a Modal Screen in the middle.

First lets rename our Stack to RootStack:

```js
// App.js

const RootStack = createStackNavigator();
```

Now below that, we declare our MainStack:

```js
// App.js

const MainStack = createStackNavigator();
```

Now let's add the MainStack and pull our existing navigation all out of the App component and into it's own MainStackScreen component:

```js
// App.js

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
// App.js

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

[🔗 Expo dc18d3d81fc5ff6a336971e8a369b5c51e11c8ec](https://github.com/kadikraman/AwesomeProjectExpo/commit/dc18d3d81fc5ff6a336971e8a369b5c51e11c8ec)

[🔗 RN 9fb150fcd1e5e2d9199f8826920d9f298de24f86](https://github.com/kadikraman/AwesomeProjectRN/commit/9fb150fcd1e5e2d9199f8826920d9f298de24f86)

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

And finally import the Modal in your App.js and add the modal to the RootStack:

```js
import AddNewPaletteModal from './screens/AddNewPaletteModal';

// place this just before </RootStack.Navigator>
<RootStack.Screen name="AddNewPalette" component={AddNewPaletteModal} />;
```

[🔗 RN 18501165c8a8f854c749da6a6d87ae0b376174a0](https://github.com/kadikraman/AwesomeProjectRN/commit/18501165c8a8f854c749da6a6d87ae0b376174a0)

[🔗 Expo 7b6e1c682eb50ab2379cb87833252897dfc65c92](https://github.com/kadikraman/AwesomeProjectExpo/commit/7b6e1c682eb50ab2379cb87833252897dfc65c92)

[👩‍💻 Live Coding a5fa145d345e29ea5005508f09bc9d143441f3c0](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/a5fa145d345e29ea5005508f09bc9d143441f3c0)
