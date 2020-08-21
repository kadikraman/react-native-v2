---
path: '/the-expo-debate'
title: 'Should you use Expo or plain React Native?'
order: 2
section: 'Introduction'
description: 'We discuss the benefits and drawback of using Expo'
---

If you've been eyeing up the React Native space already, you've probably heard of [Expo](https://expo.io/). Expo is essentially a suite of tools build for and around React Native, designed to improve and enhance the developer experience. They are a separate company, not affiliated with Facebook.

Some people have strong options on whether or not they want to use Expo for React Native, and if you're one of those people, feel free to skip this and carry on with your preference. This is an introductory workshop and can be followed with Expo and without. However if you don't have any strong opinions on this and need help deciding, read on!

If you are completely new to mobile development and just want to get a taste of React Native without a lot of upfront configuration work, I'd recommend starting with Expo, just because you'll get to the part where you try out coding much quicker.

You should also definitely go for Expo if you have a Windows or Linux machine, but you want to run the app on your physical iPhone. This is simply not possible with plain React Native, because native iOS apps can _only_ be built on a macOS machine. Expo overcomes this be allowing you to install a native "shell" app on your phone and transfer the JavaScript bundle you're working on directly into this native shell. This way, you end up only writing JavaScript on locally, no native compilation step necessary.

It can take quite a bit time to set up your development environment without Expo, since you'll have to download, install and configure XCode and/or Android Studio. Just to give you an idea of the setup time, here are some really rough estimates based on my experience:

#### macOS

- Expo on physical device: ~10 minutes (Android or iOS)
- Expo on iOS simulator: ~1 hour
- Expo on Android emulator: ~1.5 hours
- Plain React Native on physical device: ~2 hours (Android or iOS)
- Plain React Native on iOS simulator: ~2 hours
- Plain React Native on Android emulator: ~2 hours

#### Windows or Linux

- Expo on physical device: ~20 minutes (Android or iOS)
- Expo on iOS simulator: ❌
- Expo on Android emulator: ~2 hours
- Plain React Native on physical device: ~2.5 hours (Android only)
- Plain React Native on iOS simulator: ❌
- Plain React Native on Android emulator: ~3 hours

Expo restrictions only really come to play when you're doing advanced things with React Native. In particular, if you need to make any _native_ changes to your code. Basically if you need to install any libraries or add anything that changes any of the non-JavaScript code or configurations. You'll have to eject from the Expo safe space and start managing all your native code yourself as you would with plain React Native.

In my experience, all the production apps I've working on have had to be ejected, even if they started with Expo. However it has been an invaluable tool for learning and quick prototyping. I always use Expo for in-person workshops primarily because it'd be a mighty boring workshop if we all spent 2+ hours just setting up our development environment, but also because I have been using a MacBook for the past 5 years and am not confident I can always help debug issues specific to Windows and Linux. For client projects, I have always used plain React Native, usually due to the client's preference.
