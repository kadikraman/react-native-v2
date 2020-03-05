---
path: '/network-requests-exercise-solution'
title: 'Network Requests Exercise 👀'
order: 24
section: 'Hooks and Network Requests'
description: 'Network requests exercise solution'
---

[🔗 RN 657a889](https://github.com/kadikraman/AwesomeProjectRN/commit/657a8893066e7d3f197941d569c4393ba5321274)

In this exercise, we've used all 3 hooks we just learnt about!

```js
const [palettes, setPalettes] = useState([]);

const handleFetchPalettes = useCallback(async () => {
  const response = await fetch(URL);
  if (response.ok) {
    const palettes = await response.json();
    setPalettes(palettes);
  }
}, []);

useEffect(() => {
  handleFetchPalettes();
}, []);
```

First, we initialise a `useState` with an empty array to store the fetched color palettes. Make sure to also update the FlatList data prop to use the new `palettes` variable.

Then we create the actual function that does the network request. The `fetch` keyword works in React Native the same way it does on the web (with the exception that you can't get CORS errors). We fetch the data from the api, check that we received a non-error response, and save the response to the `palettes` variable which will automatically update out UI.

Finally, we add a `useEffect` which will trigger the `handleFetchPalettes` function when the component is first rendered.
