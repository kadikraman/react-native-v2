---
path: '/debugging'
title: 'Debugging'
order: 5
section: 'Setup'
description: 'How to debug code'
---

As developers, we spend a whole lot of time debugging, especially when learning something new. Here are some debugging tips for React Native.

### Debug menu

- on device - shake the device (yes, really!)
- iOS simulator - Cmd + D
- Android emulator - Cmd + M on Mac, Crl + M on Windows/Linux

<div style="display:flex; flex-direction:row">
    <div style="width:300px;margin:0 auto;margin-bottom:20px">
        <img alt="Style challenge iOS" src="./images/debugging-ios.png" />
    </div>
    <div style="width:300px;margin:0 auto;margin-bottom:20px">
        <img alt="Style challenge Android" src="./images/debugging-android.png" />
    </div>
        <div style="width:300px;margin:0 auto;margin-bottom:20px">
        <img alt="Style challenge Android" src="./images/debugging-expo.png" />
    </div>
</div>

The debug menus for iOS, Android and Expo look a bit different per platform, but they all have the same options available.

The main options you'll use are:

- refresh: this reloads the JavaScript bundle. You can also do this with Cmd + R (or Ctrl + R)
- debug: this opens a debug window in your browser
- show/hide inspector: this allows you to inspect individual elements on the page
- enable/disable fast refresh: you might now this as "hot reloading", it will update your app with your changes when you save the file, no need to refresh manually

### console.log() debugging

The easiest and most straightforward way to debug things is always the good old trusted logger! The good news is that console.log() works just the same on React Native as in plain JavaScript.

In order to log out to the console:

1. open the debug menu (as described above) and turn on the debug. This will open a new browser window
2. inspect the browser window (right click + inspect for most browsers)
3. `console.log()` something in your app
4. the logged out text will appear in the browser console!

Note:

- `console.warn` will show a yellow box warning in React Native
- `console.error` will show a full screen error
