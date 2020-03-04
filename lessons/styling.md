---
path: '/styling'
title: 'Styling'
order: 8
section: 'Basic components'
description: 'Adding styling to React Native components'
---

In React Native, all styling is done using inline styles. Let's start by adding some spacing around our content. Import `StyleSheet` from `react-native` and create a styles constant at the bottom of the file:

```js
// App.js
const styles = StyleSheet.create({
  container: {
    padding: 10,
  },
});
```

React Native styles are actually very similar to css styles on the web. The debugger also displays helpful error messages when you try to add styles that don't exist on a particular component type.

`StyleSheet.create` creates an optimized style object where you can access the individual styles like on a regular object. In this case, `styles.container` would give you all the container styles. Now all that's left to do is to pass these styles into the component. We do this using the `style` prop. Pass the container styles into our `<View>`. Your code should now look like this:

```js
// App.js

import React from 'react';
import { View, Text, SafeAreaView, StyleSheet } from 'react-native';

const App = () => {
  return (
    <SafeAreaView>
      <View style={styles.container}>
        <Text>Hello, world!</Text>
      </View>
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    padding: 10,
  },
});

export default App;
```

Very stylish! This is pretty similar to the web, only we omit the units (`px`, `em`, `rem` etc), because all dimensions in React Native are unitless, and represent density-independent pixels.

Adding a background colour for the component while your debugging can help understand positioning. Let's also add a background colour to our View before continuing:

```js
const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    padding: 10,
  },
});
```

Notice that the style names in React Native are in camelCase instead of kebab-case, but otherwise are the same as the web!

Now let's try adding different padding to the top and sides? Let's do 50 on the top and 10 on the sides. You might do something like this:

```js
const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    paddingTop: 50,
    paddingLeft: 10,
    paddingRight: 10,
  },
});
```

This works well enough, but in React Native we also have a shorthand way to set equal padding to left an right - `paddingHorizontal`. You can replace `paddingLeft` and `paddingRight` with a single `paddingHorizontal` like so:

```js
const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    paddingTop: 50,
    paddingHorizontal: 10,
  },
});
```

There is also `paddingVertical` for setting just top and bottom padding, and there are also equivalent style properties for margin: `marginHorizontal` and `marginVertical`.

[🔗 RN 931eebc](https://github.com/kadikraman/AwesomeProjectRN/commit/931eebc6558c65a9c66c6fcb3bbe63386ec0204c)

## Positioning

In React Native, all positioning is done using FlexBox and all elements have `display: flex` applied by default. If you've not used flex much before it may seem a bit daunting, but the basics are not too tricky to grasp. If you have time, [FlexBox froggy](https://flexboxfroggy.com/) is a fun little game that introduce you to the flex iteratively while you move frogs around the pond. For everyday reference [this guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) from CSS Tricks is pretty handy.

Let's update our container so that all the text is in the center of the screen. First, let's center the text horizontally.

```js
const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    alignItems: 'center',
  },
});
```

That was easy! `alignItems: 'center'` will center any content inside it horizontally. Now let's also center the content vertically.

```js
const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    alignItems: 'center',
    justifyContent: 'center',
    height: 100,
  },
});
```

This centers the content inside the lavender box. Notice we needed to se the height of the box in order for this to work. But how could we do it so the box is full height? We use `flex: 1`. Adding `flex: 1` to the container itself won't work though, because it means that the component should take the whole height of it's parent, but it's parent is a `SafeAreaView` that has no height. We'll also have to set `flex: 1` to the `SafeAreaView`. Let's try something different and do it _inline_!

```js
// App.js

import React from 'react';
import { View, Text, SafeAreaView, StyleSheet } from 'react-native';

const App = () => {
  return (
    <SafeAreaView style={{ flex: 1 }}>
      <View style={styles.container}>
        <Text>Hello, world!</Text>
      </View>
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    alignItems: 'center',
    justifyContent: 'center',
    flex: 1,
  },
});

export default App;
```

Great work! Using styles inline is handy especially when you have dynamic styles (e.g having to set the height or colour of the element dynamically), but generally we try to use the StyleSheet for styles, has some optimizations that are lost otherwise.

[🔗 RN 05e9509](https://github.com/kadikraman/AwesomeProjectRN/commit/05e9509779347160320075a2cce630c7cbe00636)

### Side note: Styled Components

If you are a fan of styled components, you might be excited to know that they have React Native support! Styling native elements looks pretty much the same as on the web, only instead of:

```js
import styled from 'styled-components';

const StyledDiv = styled.div`
  background-color: lavender;
`;
```

You'll have to do:

```js
import styled from 'styled-components/native';

const StyledView = styled.View`
  background-color: lavender;
`;
```

Otherwise the experience is exactly the same! You can even use `snake-case` like on the web! For this workshop, we will use StyleSheet, buy feel free to explore this in your own time. Read more about it [here](https://styled-components.com/docs/basics#react-native).
