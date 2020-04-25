---
path: '/network-requests-exercise-solution'
title: 'Network Requests Exercise Solution 👀'
order: 23
section: 'Hooks and Network Requests'
description: 'Network requests exercise solution'
---

[🔗 Expo 7d9e2920cce72f29547d8f6b113a31dac44da696](https://github.com/kadikraman/AwesomeProjectExpo/commit/7d9e2920cce72f29547d8f6b113a31dac44da696)

[🔗 RN 6cbb5e4895a2c8e65928cf998865a5d1062bc6bc](https://github.com/kadikraman/AwesomeProjectRN/commit/6cbb5e4895a2c8e65928cf998865a5d1062bc6bc)

[👩‍💻 Live Coding 58cae1baaa963249697ac3f30d457e0ab1a8f635](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/58cae1baaa963249697ac3f30d457e0ab1a8f635)

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
