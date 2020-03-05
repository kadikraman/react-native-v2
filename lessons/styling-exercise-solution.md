---
path: '/styling-exercise-solution'
title: 'Styling Exercise Solution 👀'
order: 10
section: 'Basic components'
description: 'We look at the solution for the styling exercise'
---

Lets start from a clean slate again.

Delete all the code in your `App.js` and replace it with the Hello World template we used earlier:

```js
import React from 'react';
import { View, Text, SafeAreaView, StyleSheet } from 'react-native';

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

Now the first thing you'll want to do is add some padding to the container. Let's to 50 from the top and 10 from the sides:

```js
const styles = StyleSheet.create({
  container: {
    paddingTop: 50,
    paddingHorizontal: 10,
  },
});
```

Now it's time to add the new text. Since we already have some text on the page, we can do this by replacing the copy for our "Hello, world!" message and adding the style:

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

Now for lets add a box for cyan. For this we need to add a new `View` and a `Text` with styles. Remember we'll have to use flex to position the text inside the boxes!

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
    paddingTop: 50,
    paddingHorizontal: 10,
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

Finally add boxes for the remaining colours (magenta and orange) the same way, and we're all done!

[🔗 RN 6e25403](https://github.com/kadikraman/AwesomeProjectRN/commit/6e25403f495a7cf7cc70cd5f177ce01379300556)
