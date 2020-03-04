---
path: '/lists'
title: 'Lists'
order: 11
section: 'Basic components'
description: 'Adding lists to React Native components'
---

What if instead of 4 colors, we had 10 or even 100? How would we display them then? If you're already familiar with React, you might be tempted to add all the colors in an array and `.map` over them. This is a very common mistake for newcomers to React Native. While it may be fine to do on the web, in React native you should avoid using map in the render. This is because mapping over an array is not optimized. React Native will attempt to render every single element in the array all at once, regardless of whether they are visible on the screen or not.

There are special components in React Native for rendering lists: these are [FlatList](https://reactnative.dev/docs/flatlist) and [SectionList](https://reactnative.dev/docs/sectionlist).

### FlatList

FlatList has a whole bunch of configuration options, but the minimum you will need to give it 3 props:
- data - this is the array of data you want to map over
- renderItem - this is a function that is passed the item and it's index and will return the individual item component
- keyExtractor - this is a function that gets passed an item and it's index

[🔍 FlatList example](https://snack.expo.io/@kadikraman/flatlist-example)

In this FlatList example, you'll see an array of foods being displayed using a FlatList.

### SectionList

SectionList is a similar to FlatList, but it allows you to render items in sections with a header item between. The data for the SectionList is still an array, but each array item will need to be an object with a title (a string) and a data (an array) prop.

Additionally you can pass in a prop called `renderSectionHeader` which will let you render the title for each section.

[🔍 SectionList example](https://snack.expo.io/@kadikraman/sectionlist-example)

This is incredibly powerful and provides a really nice native experience for the user on the device.