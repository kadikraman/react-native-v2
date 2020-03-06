---
path: '/forms-exercise-solution'
title: 'Form exercise solution 👀'
order: 28
section: 'Forms'
description: 'Solution to the Forms exercise'
---

[🔗 Expo 04d7c8fc4b9d9ad9550f541f256136487f840fa9](https://github.com/kadikraman/AwesomeProjectExpo/commit/04d7c8fc4b9d9ad9550f541f256136487f840fa9)

[🔗 RN 709f85b03bead57852da3a29fc7515bbb2219afc](https://github.com/kadikraman/AwesomeProjectRN/commit/709f85b03bead57852da3a29fc7515bbb2219afc)

The main difficulty in this exercise is the issue of how to keep track of the value of so many toggle buttons. They key is to build an update function that can handle it. The switch component can return both the color the user is interacting with and whether they turned the switch on or off. This makes things simples for us, so we can add the color to the color array if they turned to switch on, and remove it otherwise:

```js
const [selectedColors, setSelectedColors] = useState([]);

const handleUpdate = useCallback(
  (color, newValue) => {
    if (newValue === true) {
      setSelectedColors(current => [...current, color]);
    } else {
      setSelectedColors(current =>
        current.filter(c => c.colorName !== color.colorName),
      );
    }
  },
  [selectedColors, setSelectedColors],
);
```

Then, to figure out the value for the `Switch`, you san check whether the current color exists in `selectedColors`. Note that !! is a shorthand for making the value a boolean, so `!!undefined === false` and `!!{} === true`

```js
<Switch
  value={!!selectedColors.find(color => color.colorName === item.colorName)}
  onValueChange={newValue => handleUpdate(item, newValue)}
/>
```

The other difficulty is how to pass the color palette back to the Home screen. You might be tempted to do it using a callback, like so:

```js
navigation.navigate('AddNewPalette', { onSubmit: handleSubmit });
```

This will work, but you will yet a yellow box warning that you shouldn't do it. Instead, you should use the navigation prop:

```js
const newPalette = { ... };
navigation.navigate('Home', { newPalette });
```

This will make the `newPalette` prop available on the home screen via the `route`:

```js
const newPalette = route.params ? route.params.newPalette : null;
```

You'll have to make sure `route.params` exist here, because they don't by default.

Finally, we can now use `useEffect` to update the palettes and add the new one:

```js
useEffect(() => {
  if (newPalette) {
    setPalettes(current => [newPalette, ...current]);
  }
}, [newPalette]);
```

Notice that we added `[newPalette]` as the second argument - this means that the effect is run once on launch, and then if and only if the value of `newPalette` changes.

### Adding more functionality

That's all for now! You could take this little application further and add some enhancements of your own. Here are some ideas:

- copy the hex code of a color to clipboard when the user taps on it - [docs](https://reactnative.dev/docs/clipboard)
- display a preview of the colors in the modal so the user can see what they're picking
- disable the button if the form is invalid