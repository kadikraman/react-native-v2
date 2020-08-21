---
path: '/adding-navigation'
title: 'Adding Navigation'
order: 18
section: 'Navigation'
description: 'We use react-navigation to navigate to a new page and back'
---

There are two main types of navigation on mobile: bottom navigation, and stack navigation. You've certainly seen bottom navigation before, most apps have it: these are navigation items at the bottom of the screen and allow you to navigate between different sections of the app. Open the Twitter app for instance. (If you don't use Twitter, open Facebook, Instagram, Headspace, Spotify - most any app really, they all work the same regardless of whether they're build with React Native or not) Notice we have 4 bottom navigation items: home, search, notifications and messages. Notice also that navigating between them is pretty instant. When the app is launched, _all_ the root pages of the bottom navigation get rendered at once. This is something to be mindful of if you're doing a lot of network requests on your root pages.

Now make sure you're on the home page of the twitter app and press on a tweet. Notice that the home icon is still selected, we've not navigated away from Home, but we've _pushed_ another page onto the stack. This is the tweet detail screen. Most root pages on the bottom navigator are stacks. Notice also that this screen has a back button so we can navigate back to our root page. Leave the tweet detail page selected and move from home to search and back - notice that the tweet detail page is still selected even though we navigated away? That's something to be mindful of.

We don't need a bottom navigator yet, let's start with a single stack and two screens: `Home` and `ColorPalette`. First things first, let's install the npm module for the stack navigator:

```js
npm install @react-navigation/stack
```

Create a new folder in your project called `screens` and add two files: `Home.js` and `ColorPalette.js`.

Open the `Home.js` and add some text to render:

```js
// screens/Home.js

import React from 'react';
import { View, Text } from 'react-native';

const Home = () => {
  return (
    <View>
      <Text>Solarized</Text>
    </View>
  );
};

export default Home;
```

We don't need to use `SafeAreaView` anymore, since the navigation library handles the spacing above the screen for us.

Next, open `ColorPalette.js` and copy the code from `App.js` that renders the list of colors:

```js
// screens/ColorPalette.js

import React from 'react';
import { Text, StyleSheet, FlatList } from 'react-native';
import ColorBox from '../components/ColorBox';

const COLORS = [
  { colorName: 'Base03', hexCode: '#002b36' },
  { colorName: 'Base02', hexCode: '#073642' },
  { colorName: 'Base01', hexCode: '#586e75' },
  { colorName: 'Base00', hexCode: '#657b83' },
  { colorName: 'Base0', hexCode: '#839496' },
  { colorName: 'Base1', hexCode: '#93a1a1' },
  { colorName: 'Base2', hexCode: '#eee8d5' },
  { colorName: 'Base3', hexCode: '#fdf6e3' },
  { colorName: 'Yellow', hexCode: '#b58900' },
  { colorName: 'Orange', hexCode: '#cb4b16' },
  { colorName: 'Red', hexCode: '#dc322f' },
  { colorName: 'Magenta', hexCode: '#d33682' },
  { colorName: 'Violet', hexCode: '#6c71c4' },
  { colorName: 'Blue', hexCode: '#268bd2' },
  { colorName: 'Cyan', hexCode: '#2aa198' },
  { colorName: 'Green', hexCode: '#859900' },
];

const ColorPalette = () => {
  return (
    <FlatList
      style={styles.container}
      data={COLORS}
      keyExtractor={item => item.hexCode}
      renderItem={({ item }) => (
        <ColorBox hexCode={item.hexCode} colorName={item.colorName} />
      )}
      ListHeaderComponent={<Text style={styles.heading}>Solarized</Text>}
    />
  );
};

const styles = StyleSheet.create({
  container: {
    padding: 10,
  },
  heading: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
  },
});

export default ColorPalette;
```

Open the `App.js` and remove all the code we've copied away to `ColorPalette.js`.

Next, we'll want to import the Home and ColorPalette screens:

```js
import Home from './screens/Home';
import ColorPalette from './screens/ColorPalette';
```

We'll also need to create a stack navigator:

```js
import { createStackNavigator } from '@react-navigation/stack';

const Stack = createStackNavigator();
```

Finally, we want to add the stack navigator inside the `<NavigationContainer>` with our two new routes:

```js
// App.js

<NavigationContainer>
  <Stack.Navigator>
    <Stack.Screen name="Home" component={Home} />
    <Stack.Screen name="ColorPalette" component={ColorPalette} />
  </Stack.Navigator>
</NavigationContainer>
```

The main thing to note here is that we give each screen a _unique_ name. This name is important, as this is what we will be using to navigate between the screens.

Now we need to make it so when you press on the word `Solarized`, it will open our ColorPalette component. For this we have a selection of _touchable_ components to choose from:

- [TouchableOpacity](https://reactnative.dev/docs/touchableopacity) - the wrapped component has opacity applied when touch is in progress
- [TouchableHighlight](https://reactnative.dev/docs/touchablehighlight) - the wrapped component darkens when touch is in progress
- [TouchableWithoutFeedback](https://reactnative.dev/docs/touchablewithoutfeedback) - no visual feedback
- [TouchableNativeFeedback](https://reactnative.dev/docs/touchablenativefeedback) - (Android only) adds Android-style touch feedback

We will be using `TouchableOpacity`. Go ahead and wrap the text in the `Home.js` component in a `<TouchableOpacity>`. On the web, buttons have an `onClick` property. On mobile, we have an `onPress` which takes a function that will be executed when the user presses on anything inside the touchable area.

Finally, we'll need a way to tell the navigation where we'd like to go. Every component inside `Stack.Screen` will automatically get access to a special [`navigation` prop](https://reactnavigation.org/docs/navigation-prop). This is the main tool you'll be using for anything navigation-related in your app. It can do a bunch of things, like programmatically go back a screen, reset the navigation stack and much more. We will be using it to navigate to the `ColorPalette` screen. This is done by calling the `navigate` function on the prop and passing in the desired route name:

```js
// screens/Home.js

const Home = ({ navigation }) => {
  return (
    <View>
      <TouchableOpacity onPress={() => navigation.navigate('ColorPalette')}>
        <Text>Solarized</Text>
      </TouchableOpacity>
    </View>
  );
};
```

[🔗 Expo f4df234627b546758e8b573f43286e0ca73cc46b](https://github.com/kadikraman/AwesomeProjectExpo/commit/f4df234627b546758e8b573f43286e0ca73cc46b)

[🔗 RN cfdef69d85efcd0967ee35c795fc64906e2bf2c8](https://github.com/kadikraman/AwesomeProjectRN/commit/cfdef69d85efcd0967ee35c795fc64906e2bf2c8)

[👩‍💻 Live Coding 0cf28f8a982310c7a50f66c09c3e5abea55fc492](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/0cf28f8a982310c7a50f66c09c3e5abea55fc492)
