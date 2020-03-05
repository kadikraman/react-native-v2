---
path: '/navigation-expo'
title: '[Expo] Adding navigation with Expo'
order: 18
section: 'Navigation'
description: 'Adding Expo Navigation'
---

If you're using Expo, you're in luck. This setup is not nearly as tricky as pure React Native, since Expo have done all the heavy lifting for you. All you need to do is first install the navigation library:

```sh
npm install @react-navigation/native
```

and then all the expo-compatible dependencies:

```sh
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

Finally, open `App.js` and add the following:

```js
import { NavigationContainer } from '@react-navigation/native';

const App = () => {
  return (
    <NavigationContainer>{/* Rest of the app code */}</NavigationContainer>
  );
};

export default App;
```

Specifically, you are importing the `NavigationContainer` from the navigation library we just installed, and wrapping the whole application in it. That's it! We're ready to start navigating.
