---
path: '/components'
title: 'Components'
order: 10
section: 'Basic components'
description: 'Something something components'
---

React (Native) is a component-based framework. This means that your app is made from lots of components that are nested within each other. You're always have one root component (in our case it is our App component), but inside it we can have as many big or small components as we'd like.

It's generally a really good practice to break your app into components and to make the components as small and standalone as possible. This is handy because:

1. It promotes component reuse - you've already built a button once. Why not reuse it?
2. Easier to follow - no one wants to debug a 1000 line component if they can help it
3. Easier to test - the smaller the unit, the easier it is to unit test!

Look at the app we're built so far. Can you see something that could be extracted into a component and reused? I can! The coloured boxes are a great candidate.

Lets start by creating a new folder called `components` in the root level of your project directory. Generally it is a good practice to have one component per file, so we'll do that.

Inside your `components` directory, create a new file called `ColorBox.js` and open it.

Let's add some code to display the box on the screen:

```js
// components/ColorBox.js

import React from 'react';
import { View, Text } from 'react-native';

const ColorBox = () => {
  return (
    <View>
      <Text>I am a color box!</Text>
    </View>
  );
};

export default ColorBox;
```

But nothing is appearing in our app. That's because we need to import this new component into our `App.js` and add it to our code.

Open the `App.js` and add the new ColorBox component just inside the last view, under the last existing coloured box:

```js
// App.js

import ColorBox from './components/ColorBox';

// add this in a new line, just before the last </View>
<ColorBox />;
```

Now you should be able to see the text "I am a color box" in your app just under the last box!

[🔗 RN 25ec4f9](https://github.com/kadikraman/AwesomeProjectRN/commit/25ec4f94f91f27a334290c84010a99391485a4a5)

## Props

In order for our new ColorBox component to be able to reused for different colours, we'll need to somehow dynamically set it's colour. To do this, we can use `props`. Props is short for properties and is basically a way to pass information down the component tree.

Our color box will need to know two things - the name of the color and the hex code. Let's start with cyan and add these props to the `<ColorBox>` component in `App.js`:

```js
// App.js

<ColorBox hexCode="#2aa198" colorName="Cyan" />
```

These props are now available to ColorBox. Let's open ColorBox again and display the name of the color dynamically:

```js
// components/ColorBox.js

const ColorBox = props => {
  return (
    <View>
      <Text>
        {props.colorName} {props.hexCode}
      </Text>
    </View>
  );
};
```

Notice that we have to use braces `{}` around variables in order to display them inside Text. This is so React Native could distinguish between pain text and variables that should be evaluated.

Last thing we'll need to do is style the box! Remember that we can pass in an array to the `style` prop to add multiple styles!

```js
// components/ColorBox.js

import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const ColorBox = props => {
  const colorStyle = {
    backgroundColor: props.hexCode,
  };

  return (
    <View style={[styles.box, colorStyle]}>
      <Text style={styles.text}>
        {props.colorName} {props.hexCode}
      </Text>
    </View>
  );
};

const styles = StyleSheet.create({
  box: {
    padding: 10,
    borderRadius: 3,
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 10,
  },
  text: {
    fontWeight: 'bold',
    color: 'white',
  },
});

export default ColorBox;
```

[🔗 RN a4d5d24](https://github.com/kadikraman/AwesomeProjectRN/commit/a4d5d240555f97bba03c894a33ca4dcd7a30b940)

Finally, replace update all the existing colour boxes to use our new component and remove unused code, and we're done! The app looks the same, but our code is a whole lot cleaner.

[🔗 RN 0cac473](https://github.com/kadikraman/AwesomeProjectRN/commit/0cac473fef5ad176928249b83bd6aa8e6abf547e)

