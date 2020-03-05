---
path: '/lists'
title: 'Lists'
order: 12
section: 'Basic components'
description: 'Lists in React Native'
---

What if instead of 4 colors, we had 10 or even 100? How would we display them then? If you're already familiar with React, you might be tempted to add all the colors in an array and `.map` over them. This is a very common mistake for newcomers to React Native. While it may be fine to do on the web, in React Native you should avoid using map in the render. This is because mapping over an array is not optimized. React Native will attempt to render every single element in the array all at once, regardless of whether they are visible on the screen or not.

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

## List props

The list elements have a bunch of built in properties to help customize for your experience. Check out the [FlatList](https://reactnative.dev/docs/flatlist) and [SectionList](https://reactnative.dev/docs/sectionlist) docs for all of them. Here are some I tend to use most often:

- [ItemSeparatorComponent](https://reactnative.dev/docs/flatlist#itemseparatorcomponent)- renders a custom separator between your items. Handy if you have to e.g. render a line or even something dynamic instead of building it into the list items
- [ListEmptyComponent](https://reactnative.dev/docs/flatlist#listemptycomponent) - this is rendered when the `data` is an empty array or undefined. Saves you from doing conditional rendering manually!
- [ListFooterComponent](https://reactnative.dev/docs/flatlist#listfootercomponent) - renders something at the bottom of the list
- [ListHeaderComponent](https://reactnative.dev/docs/flatlist#listheadercomponent) - renders something at the top of the list
- [extraData](https://reactnative.dev/docs/flatlist#extradata) - the list only gets re-rendered if the `DATA` changes. It might happen though that what you display depends on some external factors. In this case use the `extraData` to pass in any variables that should also trigger a re-render when changed
- [horizontal](https://reactnative.dev/docs/flatlist#extradata) - render the list horizontally instead of vertically
- [numColumns](https://reactnative.dev/docs/flatlist#extradata) - render multiple columns
- [onEndReached](https://reactnative.dev/docs/flatlist#extradata) - fires when the user has scrolled to the end of the list. Handy for pagination
