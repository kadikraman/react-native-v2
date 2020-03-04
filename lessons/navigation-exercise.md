---
path: '/navigation-exercise'
title: 'Navigation Exercise 📝'
order: 16
section: 'Navigation'
description: 'Passing parameters'
---

You can pass down parameters to the screen you navigate to as a second argument:

```js
const COLORS = [...];

navigation.navigate('ColorPalette', { paletteName: 'Solarized', colors: COLORS })`;
```

This will make the paletteName and colors available to the ColorPalette via the `route` prop:

```js
// ColorPalette.js

console.log(route.params.paletteName);

// logs out: Solarized
```

For this exercise:

1. update the app so that the colors and name are being passed into the ColorPalette component, making it reusable. [Docs](https://reactnavigation.org/docs/params)
2. make sure the page title will be the name of the color palette instead of the name of the page. [Docs](https://reactnavigation.org/docs/headers#using-params-in-the-title)
3. add a Rainbow color scheme (hint: you create a `COLOR_PALETTES` array and use a `FlatList` to render them)
4. update the Home page to display the first 3 colors of the color scheme as preview (stretch goal)

```js
const RAINBOW = [
  { colorName: 'Red', hexCode: '#FF0000' },
  { colorName: 'Orange', hexCode: '#FF7F00' },
  { colorName: 'Yellow', hexCode: '#FFFF00' },
  { colorName: 'Green', hexCode: '#00FF00' },
  { colorName: 'Violet', hexCode: '#8B00FF' },
];
```

<div style="width:700px;margin:0 auto;margin-bottom:20px">
    <img alt="Completed palette preview exercise" src="./images/palette-preview.gif" width=700 />
</div>

This is a guide for what the completed exercise should looks like. Notice that the navigation is different between iOS and Android? This is because both platforms leverage the native conventions for navigation. It is what the user is expecting and provides the best experience.

## Navigation Exercise Solution - Part 1 👀

_Update the app so that the colors and name are being passed into the ColorPalette component, making it reusable._

[🔗 RN 83a3946](https://github.com/kadikraman/AwesomeProjectRN/commit/83a394603816a1fb49b0674c77984ba14d8cd012)

For this we need to move the `COLORS` constant from `ColorPalette` to `Home` and pass in both the paletteName and colors as a second argument to `navigation.navigate`.

Then in `ColorPalette`, use the `route` prop, specifically `route.params.paletteName` and `route.params.colors` to replace the previously hardcoded values.

Finally, if you haven't done so already, add `backgroundColor: 'white'` to the `container` style in `ColorPalette`. React Navigation adds a greyish background to pages by default.

## Navigation Exercise Solution - Part 2 👀

_Make sure the page title will be the name of the color palette instead of the name of the page._

[🔗 RN 921be40](https://github.com/kadikraman/AwesomeProjectRN/commit/921be406d9d22ef2dfa6def883b11059ba65d2f1)

As in the [docs](https://reactnavigation.org/docs/headers#using-params-in-the-title), open `App.js` and add an extra prop to the ColorPalette screen:

```js
options={({ route }) => ({ title: route.params.paletteName })}
```

You can also delete the `ListHeaderComponent` prop from `ColorPalette`, since the palette name is already displayed as the page title.

## Navigation Exercise Solution - Part 3 👀

_Add a Rainbow color scheme._

[🔗 RN d4809be](https://github.com/kadikraman/AwesomeProjectRN/commit/d4809bea3de506a4571f557287d5a11078ffa394)

Fist off we'll want to create a new array for `COLOR_PALETTES`:

```js
// screens/Home.js

const COLOR_PALETTES = [
  { paletteName: 'Solarized', colors: SOLARIZED },
  { paletteName: 'Rainbow', colors: RAINBOW },
];
```

Next up we can replace our existing code in the render with a single FlatList:

```js
// screens/Home.js

<FlatList
  data={COLOR_PALETTES}
  keyExtractor={item => item.paletteName}
  renderItem={({ item }) => (
    <TouchableOpacity onPress={() => navigation.push('ColorPalette', item)}>
      <Text>{item.paletteName}</Text>
    </TouchableOpacity>
  )}
/>
```

Make sure you've replaced the hardcoded values in renderItem with the dynamic ones we're done!

## Navigation Exercise Solution - Part 4 👀

Update the Home page to display the first 3 colors of the color scheme as preview

[🔗 RN 6cfd163](https://github.com/kadikraman/AwesomeProjectRN/commit/6cfd163ea3524febbd34e7f984bbd84b1bd58cd7)

Create a new component in out components directory and let's call it `PalettePreview`. Before you start adding styling and colors to it, make sure the existing functionality remains unbroken.

In the Home component, update the `renderItem` to use `PalettePreview` instead:

```js
// screens/Home.js

<PalettePreview
  onPress={() => navigation.push('ColorPalette', item)}
  palette={item}
/>
```

And in PalettePreview, copy the code that used to be in renderItem and use the passed in props to display the component name and handle onPress"

```js
// components/PalettePreview.js

import React from 'react';
import { TouchableOpacity, Text, View } from 'react-native';

const PalettePreview = ({ palette, onPress }) => {
  return (
    <TouchableOpacity onPress={onPress}>
      <Text>{palette.paletteName}</Text>
    </TouchableOpacity>
  );
};

export default PalettePreview;
```

Now, add a FlatList under the `<Text>` in `PalettePreview` to render the three preview colors. Technically you could get away with not using `FlatList` here, since we know we'll only ever have 3 items to display, but using FlatList it's a good habit to get into and there's no harm, so I'd recommend always using a `FlatList` for 3+ items.

Note, you can use `palette.colors.slice(0, 3)` to get the first 3 items of your color array (never splice, as it mutates the array).

You'll have to pass in an array of styles to the little color square in order to set the backgorund dynamically, like so:

```js
// components/PalettePreview.js

renderItem={({ item }) => (
    <View style={[styles.color, { backgroundColor: item.hexCode }]} />
)}
```
