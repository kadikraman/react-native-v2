---
path: '/navigation-rn'
title: '[RN] Adding navigation with plain React Native'
order: 16
section: 'Navigation'
description: 'Adding Navigation in plain React Native'
---

We will be following the [getting started guide](https://reactnavigation.org/docs/getting-started) on the React Navigation website. Feel free to use it as a reference.

React Navigation is what we call a "library with native dependencies". That is, it doesn't _just_ contain JavaScript code and dependencies: it also has some native to iOS and Android. This is necessary for navigation, because we want to take utilise the tools already natively available for navigation to make the user experience as seamless as possible.

First, let's install the necessary dependencies. Run this in your terminal in tour project directory:

```sh
npm install @react-navigation/native react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

### iOS

If you are building iOS, you'll need to also install the native dependencies. The package manager we will be using for iOS is called CocoaPods, or "Pods" for short. You can think of it as npm for iOS. If you look inside the `/ios` directory of your application, you'll find a `Podfile` and a `Podfile.lock` (sounds a lot like `package.json` and `package.lock`!). Prior to React Native 0.60, users had to "manually link" their native libraries. This was tedious and error prone. Now however, the dependencies are "autolinked", but you still have to install them yourself.

Check if you have CocoaPods installed by running:

```sh
pod --version
```

If not, you can install it on the terminal with:

```sh
sudo gem install cocoapods
```

This might take a little while. Once you have CocoaPods installed, navigate to the ios directory and install the pods!

```sh
cd ios
pod install
cd ..
```

### Android

If you are building for Android you won't need to install the native dependencies yourself. This is done automagically by Gradle. Gradle is not a package manager par se, but let's just say it's a build toolkit for Android. When you run your Android project for the first time, it will download all the missing or changed dependencies.

You will however need to add some dependencies yourself: open `android/app/build.gradle` and add the following under `dependencies`:

```sh
implementation 'androidx.appcompat:appcompat:1.1.0-rc01'
implementation 'androidx.swiperefreshlayout:swiperefreshlayout:1.1.0-alpha02'
```

These are just some native android tools necessary for compatibility with the latest version of the navigation library.

### Finally (both iOS and Android)

Finally, open `App.js` and add the following:

```js
import 'react-native-gesture-handler';
// other imports
import { NavigationContainer } from '@react-navigation/native';

const App = () => {
  return (
    <NavigationContainer>{/* Rest of the app code */}</NavigationContainer>
  );
};

export default App;
```

Note that the gesture handle import has to be _the very first line_ in your file, even before the React import, and the `<NavigationContainer>` wraps around the whole app.

Now you'll have to also rebuild the native application. Whenever you add a library that has native dependencies, you'll have to reinstall in order for the new library to be included in the build.

Open you terminal and run `npx react-native run-ios` or `npx react-native run-android` depending on what you're building for.

[🔗 RN 2f545f0](https://github.com/kadikraman/AwesomeProjectRN/commit/2f545f0d4d08b7efc5f44c18479312c7be450eb1)
