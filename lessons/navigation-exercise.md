---
path: '/navigation-exercise'
title: 'Navigation Exercise 📝'
order: 19
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
