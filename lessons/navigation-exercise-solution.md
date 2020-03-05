---
path: '/navigation-exercise-solution'
title: 'Navigation Exercise Solution 👀'
order: 20
section: 'Navigation'
description: 'Navigation exercise solution'
---

## Navigation Exercise Solution - Part 1

_Update the app so that the colors and name are being passed into the ColorPalette component, making it reusable._

[🔗 Expo 23c9ccc3a0943d2082e402cf5b2e524abb5fc186](https://github.com/kadikraman/AwesomeProjectExpo/commit/23c9ccc3a0943d2082e402cf5b2e524abb5fc186)

[🔗 RN 16847962f25d823c57d2f7a4c060e976ccc53df5](https://github.com/kadikraman/AwesomeProjectRN/commit/16847962f25d823c57d2f7a4c060e976ccc53df5)

For this we need to move the `COLORS` constant from `ColorPalette` to `Home` and pass in both the paletteName and colors as a second argument to `navigation.navigate`.

Then in `ColorPalette`, use the `route` prop, specifically `route.params.paletteName` and `route.params.colors` to replace the previously hardcoded values.

Finally, if you haven't done so already, add `backgroundColor: 'white'` to the `container` style in `ColorPalette`. React Navigation adds a greyish background to pages by default.

## Navigation Exercise Solution - Part 2

_Make sure the page title will be the name of the color palette instead of the name of the page._

[🔗 Expo e48d0c44a27fb335292caa98d60a4b543ea86d66](https://github.com/kadikraman/AwesomeProjectExpo/commit/e48d0c44a27fb335292caa98d60a4b543ea86d66)

[🔗 RN addcea59e9e01a60c7e7864e36f925962f25433f](https://github.com/kadikraman/AwesomeProjectRN/commit/addcea59e9e01a60c7e7864e36f925962f25433f)

As in the [docs](https://reactnavigation.org/docs/headers#using-params-in-the-title), open `App.js` and add an extra prop to the ColorPalette screen:

```js
options={({ route }) => ({ title: route.params.paletteName })}
```

You can also delete the `ListHeaderComponent` prop from `ColorPalette`, since the palette name is already displayed as the page title.

## Navigation Exercise Solution - Part 3

_Add a the new color schemes._

[🔗 Expo a530072a2fd96483522ae2773ecd60f0ccd7ccfc](https://github.com/kadikraman/AwesomeProjectExpo/commit/a530072a2fd96483522ae2773ecd60f0ccd7ccfc)

[🔗 RN d8a1624f38969e5e2b5a635c0b65032749943e1b](https://github.com/kadikraman/AwesomeProjectRN/commit/d8a1624f38969e5e2b5a635c0b65032749943e1b)

Fist off we'll want to create a new array for `COLOR_PALETTES`:

```js
// screens/Home.js

const COLOR_PALETTES = [
  { paletteName: 'Solarized', colors: SOLARIZED },
  { paletteName: 'Frontend Masters', colors: FRONTEND_MASTERS },
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

## Navigation Exercise Solution - Part 4

Update the Home page to display the first 5 colors of the color scheme as preview

[🔗 Expo ee58e627009cd65b6b351d31f0fc283b9e22c71b](https://github.com/kadikraman/AwesomeProjectExpo/commit/ee58e627009cd65b6b351d31f0fc283b9e22c71b)

[🔗 RN 00587307ee119e11bbbc0a74544969c2bd5da87e](https://github.com/kadikraman/AwesomeProjectRN/commit/00587307ee119e11bbbc0a74544969c2bd5da87e)

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

You'll have to pass in an array of styles to the little color square in order to set the background dynamically, like so:

```js
// components/PalettePreview.js

renderItem={({ item }) => (
    <View style={[styles.color, { backgroundColor: item.hexCode }]} />
)}
```

Finally, in order to ensure that the white palette colors still show up on the white background, add a shadow:

```js
shadowColor: '#000',
shadowOffset: { width: 0, height: 1 },
shadowOpacity: 0.3,
shadowRadius: 1,
elevation: 2,
```

`elevation: 2` is Android only and the rest is iOS only.
