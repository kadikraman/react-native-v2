---
path: '/page-2'
title: '[Expo] Getting started with Expo'
order: 3
section: 'Setup'
description: 'Getting started with Expo'
---

The fastest way to get started with React Native is to us Expo and run the app on your device. Feel free to use the [React Native docs](https://reactnative.dev/docs/getting-started) or [Expo docs](https://docs.expo.io/versions/latest/) for reference.

#### You'll need:

- a computer (Mac, Windows or Linux)
- a smartphone (iPhone or Android)

### Install Node

First, make sure you have Node.js installed (10.0 or later). You can do this by opening a terminal and running `node -v`. If not you can install it [here](https://nodejs.org/en/). There's usually two version to choose from, pick the one that says LTS (Long Term Support) after the version number.

### Install Expo

```sh
npm install -g expo-cli
```

This installs the expo cli globally. We'll be using this to create our new project.

### Create the project

```sh
expo init AwesomeProject
```

You'll be prompted to choose a template. Pick the 'blank' - we're starting from scratch!

### Run the project

```sh
cd AwesomeProject
npm start
```

Note that you can also use `expo start` or `yarn start` if you have yarn installed.

### Preview the app on your phone

First, make sure that your phone is connected to the same WiFi network as your computer. This is really important!

Next you'll need to install the Expo client on your phone. This is the native shell Expo provides that lets you get started without having the build the native app yourself. Go to the App Store or Play store, search for "Expo" and install it. You will also have to create an Expo account if you don't already have one (don't worry - it's free!).

Finally, open the browser window that was opened when you ran the packages. See the QA code? If you're on Android, you can scan the code with your Expo app. On iOS, open the camera app to can the code. You will be prompted to "open in Expo".

At this point you should see something like this:

<div style="width:250px;margin:0 auto;margin-bottom:20px">
    <img alt="Expo hello world" src="./images/expo-init.png" />
</div>

And that's it! You're ready to start coding!
