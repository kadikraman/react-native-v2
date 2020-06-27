---
path: '/styling'
title: 'Styling'
order: 8
section: 'Basic components'
description: 'We talk about styling React Native components'
---

In React Native, all styling is done using inline styles. We use a `StyleSheet` from `react-native` to create the styles. Usually we add this styles constant at the bottom of the file, or in a separate file:

```js
const styles = StyleSheet.create({
  container: {
    padding: 10,
  },
});
```

React Native styles are actually very similar to css styles on the web. The debugger also displays helpful error messages when you try to add styles that don't exist on a particular component type.

`StyleSheet.create` creates an optimized style object where you can access the individual styles like on a regular object. In this case, `styles.container` would give you all the container styles. Now we can use this style prop inside our JSX by passing it into the relevant element:

```js
<View style={styles.container}>
  <Text>Hello, world!</Text>
</View>
```

This is pretty similar to the styles on the web, only we omit the units (`px`, `em`, `rem` etc), because all dimensions in React Native are unitless, and represent density-independent pixels.

Adding a background colour for the component while your debugging can help understand positioning. We could add a background color using the `backgroundColor` property:

```js
const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    padding: 10,
  },
});
```

Note that all the web colors will work here, but we can also use hex `#ffffff` or rgb `rgb(255,255,255)` or rgba `rgba(255,0,0,0.3)`.

Notice that the style names in React Native are in camelCase instead of kebab-case, but otherwise are the same as the web!

The style properties you can use depend on the component you're trying to style, and fall into 3 categories:

- [View style props](https://reactnative.dev/docs/view-style-props)
- [Text style props](https://reactnative.dev/docs/text-style-props)
- [Image style props](https://reactnative.dev/docs/image-style-props)

There are some special properties you might not have seen on the web. For instance, you will frequently find yourself applying the same padding or margin. There is a shorthand for it on the web where you can do `margin: 10, 20`, but this won't fly here, since we use number, not strings. Instead, we can set the styles to be `horizontal` or `vertical`. So instead of writing this:

```js
const styles = StyleSheet.create({
  container: {
    paddingLeft: 10,
    paddingRight: 10,
    marginTop: 20,
    marginBottom: 20,
  },
});
```

We can write this:

```js
const styles = StyleSheet.create({
  container: {
    paddingHorizontal: 10,
    marginVertical: 20,
  },
});
```

## Positioning

In React Native, all positioning is done using FlexBox and all elements have `display: flex` applied by default. If you've not used flex much before it may seem a bit daunting, but the basics are not too tricky to grasp. If you have time, [FlexBox froggy](https://flexboxfroggy.com/) is a fun little game that introduce you to the flex iteratively while you move frogs around the pond. For everyday reference [this guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) from CSS Tricks is pretty handy.

Suppose we wanted to center all content in a container horizontally. For this, we can use `alignItems: 'center`:

```js
const styles = StyleSheet.create({
  container: {
    alignItems: 'center',
  },
});
```

To center all content in a container vertically, we can use `justifyContent: 'center'`. We'll also have to use `flex: 1` to ensure the component takes up the whole height of the screen. If the component is nested inside another component, you'll have to make sure the other component also has `flex: 1`:

```js
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
  },
});
```

## Styles without StyleSheet

You should always aim to write your styles in a StyleSheet, but sometimes it's not possible or just sub-optimal. For example if you had to add styles dynamically. In this case, we can pass styles into the component as plain objects like so:

```js
<View style={{ backgroundColor: 'teal' }} />
```

Notice the double braces? The first set of braces is to tell JSX we're passing in an object and the second is for the actual object. This is equivalent:

```js
const componentStyle = { backgroundColor: 'teal' };

<View style={componentStyle} />;
```

## Multiple styles in one component

Sometimes you may want to add multiple style objects to one element. You can do this by passing in an _array_ of styles instead of a single style like so:

```js
<View style={[styles.firstStyle, styles.secondStyle]} />
```

The styles cascade as they would on the web, so the later styles would override the former if there are any repeats.

You can also mix `StyleSheet` styles and object styles:

```js
<View style={[styles.firstStyle, { backgroundColor: 'teal' }]} />
```

## Side note: Styled Components

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

Otherwise the experience is exactly the same! You can even use `snake-case` like on the web! For this workshop, we will use `StyleSheet`, but feel free to explore this in your own time. Read more about it [here](https://styled-components.com/docs/basics#react-native).
