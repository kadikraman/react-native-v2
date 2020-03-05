---
path: '/ejecting-from-expo'
title: '[Expo] Ejecting from Expo'
order: 29
section: 'Extra Credit'
description: 'Why and how you might need or want to eject from Expo'
---

Living in the Expo sandbox is fantastic, especially when you're just getting started, prototyping, or building MVPs. There are restrictions that come with all this convenience however, the main one is not being able to use any native libraries that are not already built into Expo.

At this point you'll have to eject. Now, that does that mean? Effectively it's more flexibility and also more work for you:

- you'll have the build deploy, manage native dependencies yourself
- you can no longer use the Expo app the preview your code

In order to eject, navigate to the root directory of your expo project and run:

```sh
expo eject
```

This will create `/ios` and `/android` directories with all the native code that Expo was managing for you. You can edit the code now, but you'll have to build and run your app yourself. You can reference the [plain RN instructions](./setup-rn) for getting set up on your device or emulator. Specifically, you'll now have to build the native bundle yourself, download Xcode and/or Android Studio and emulators/simulators.

Read more about ejecting [here](https://docs.expo.io/versions/latest/expokit/eject/).
