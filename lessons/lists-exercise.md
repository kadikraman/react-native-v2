---
path: '/lists-exercise'
title: 'Lists Exercise 📝'
order: 11
section: 'Basic components'
description: 'Lists challenge'
---

You might have already recognized the colours we were using earlier. They are part of the [Solarized](<https://en.wikipedia.org/wiki/Solarized_(color_scheme)>) color scheme by Ethan Schoonover. The colour palette actually contains 16 colours and next up, we'd like to display them all:

```js
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
```

You should be using FlatList for this.

For extra credit - also display the name of the color in white on the darker colors and in black on the lighter ones!

<div style="display:flex; flex-direction:row">
    <div style="width:400px;margin:0 auto;margin-bottom:21px">
        <img alt="List exercise iOS" src="./images/ios-list-exercise.png" />
    </div>
    <div style="width:400px;margin:0 auto;margin-bottom:21px">
        <img alt="List exercise Android" src="./images/android-list-exercise.png" />
    </div>
</div>

## Lists Exercise Solution 👀

[🔗 RN 6edd87e](https://github.com/kadikraman/AwesomeProjectRN/commit/6edd87e4cc8b661f10c3cf87c1486b0a116fc368)

In this solution we're removed the individual `ColorBox`es and rendered them all using a `FlatList`. Some things to note:

- since we no longer have a containing div, we not pass in the component styles into the `FlatList` component instead. Almost all native components in React Native can by styled using the style prop
- notice that the name of the palette scrolls with the colors. This is because we added it to FlatList using the `ListHeaderComponent` prop
- we've used a little calculation to adjust text colour for the background colour. There are better algorithms to do this, but this si certainly the shortest: `parseInt(props.hexCode.replace('#', ''), 16) > 0xffffff / 1.1`. Here we essentially get the lightest 10% of the background colors and display black text for these, and white for the rest.
