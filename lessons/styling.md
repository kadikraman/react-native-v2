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

Very stylish! Now let's try adding different padding to the top and sides? Let's do 50px on the top and 10px on the sides. You might do something like this:

```js
const styles = StyleSheet.create({
  container: {
    paddingTop: 50,
    paddingLeft: 10,
    paddingRight: 10,
  },
});
```

Notice that this looks quite similar to css only we use camelCase instead of kebab-case, and we use numbers for pixel values and there is no need to add the unit (e.g. `px`) in the end.

This works well enough, but in React Native we also have a shorthand way to set equal padding to left an right - `paddingHorizontal`. You can replace `paddingLeft` and `paddingRight` with a single `paddingHorizontal` like so:

```js
const styles = StyleSheet.create({
  container: {
    paddingTop: 50,
    paddingHorizontal: 10,
  },
});
```

There is also `paddingVertical` for setting just top and bottom padding, and there are also equivalent style properties for margin: `marginHorizontal` and `marginVertical`.

## Coding Challenge 💪

The best way to learn is by doing so let's start off by adding some colour. Here's a little app I built, showcasing come of my favourite colours. Try to recreate it! Here are the colours I used:

```
Cyan: #2aa198
Blue: #268bd2
Magenta: #d33682
Orange: #cb4b16
```

<div style="display:flex; flex-direction:row">
    <div style="width:400px;margin:0 auto;margin-bottom:20px">
        <img alt="Style challenge iOS" src="./images/style-ios.png" />
    </div>
    <div style="width:400px;margin:0 auto;margin-bottom:20px">
        <img alt="Style challenge Android" src="./images/style-android.png" />
    </div>
</div>

## Coding challenge - solution

First thing we want to do is add the new text. Since we already have some text on the page, we can do this by replacing the copy for our "Hello, world!" message and adding the style:

```js
// replace "hello world" text and add style prop

<Text style={styles.heading}>Here are some boxes of different colours</Text>
```

```js
// place this in the stylesheet, under the container style

heading: {
  fontSize: 18,
  fontWeight: 'bold',
  marginBottom: 10,
}
```

Now for lets add a box for cyan. For this we need to add a new `View` and a `Text` with styles. One thing to note about styling in React Native is that all elements have `display: flex` applies by default so all positioning should be done using felxBox. If you're new to flexBox, here are some resources TODO: link to flexbox froggy and flex documentation.

You can use `justifyContent: 'center'` and `alignItems: 'center'` on the parent element to center content both horizontally and vertically.

```js
<View style={styles.cyanBox}>
  <Text style={styles.text}>Cyan #2aa198</Text>
</View>
```

```js
text: {
  fontWeight: 'bold',
  color: 'white'
},
cyanBox: {
  padding: 10,
  borderRadius: 3,
  justifyContent: 'center',
  alignItems: 'center',
  marginBottom: 10,
  backgroundColor: '#2aa198'
}
```

Looking good! Let's add the blue box as well. Your `App.js` now looks something like this:

```js
// App.js

import React from 'react';
import { View, Text, SafeAreaView, StyleSheet } from 'react-native';

const App = () => {
  return (
    <SafeAreaView>
      <View style={styles.container}>
        <Text style={styles.heading}>
          Here are some boxes of different colours
        </Text>
        <View style={styles.cyanBox}>
          <Text style={styles.text}>Cyan #2aa198</Text>
        </View>
        <View style={styles.blueBox}>
          <Text style={styles.text}>Blue #268bd2</Text>
        </View>
      </View>
    </SafeAreaView>
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
  text: {
    fontWeight: 'bold',
    color: 'white',
  },
  cyanBox: {
    padding: 10,
    borderRadius: 3,
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 10,
    backgroundColor: '#2aa198',
  },
  blueBox: {
    padding: 10,
    borderRadius: 3,
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 10,
    backgroundColor: '#268bd2',
  },
});

export default App;
```

This is looking good, but you might have noticed there are a lot of repeated styles between the two boxes and this can get cumbersome pretty quickly. Thankfully there is a way around this. The `style` prop also accepts an _array_ of styles, so instead of `style={styles.cyanBox}` we could pass in two sets of styles: `style={[styles.box, styles.cyan]}`.

```js
<View style={[styles.box, styles.cyan]}>
    <Text style={styles.text}>Cyan #2aa198</Text>
</View>
<View style={[styles.box, styles.blue]}>
    <Text style={styles.text}>Blue #268bd2</Text>
</View>
```

```js
box: {
  padding: 10,
  borderRadius: 3,
  justifyContent: 'center',
  alignItems: 'center',
  marginBottom: 10,
},
cyan: {
  backgroundColor: '#2aa198'
},
blue: {
  backgroundColor: '#268bd2'
},
```

Finally add the remaining colours. The finished code should look something like this. (TODO: link to example app)
