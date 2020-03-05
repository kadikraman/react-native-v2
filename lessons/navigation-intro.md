---
path: '/navigation-intro'
title: 'Navigation Into'
order: 15
section: 'Navigation'
description: 'Introduction to navigation'
---

Now it's time to add navigation to our app. Let's start with adding a new page where we could list _multiple_ color schemes as a list, and then navigate to a new page to view their details.

In order to achieve this, we will need a way to navigate between screens.

You may be surprised to learn that React Native does not actually come with any navigation tools. Despite the fact that pretty much every React Native application has navigation, it's not bundled into the framework and you'll have to install it separately. This is because Facebook have their own in-house navigation solution which is really customized for their own use case, so there was no way to share it for general use.

There are two popular libraries to choose from: [React Navigation](https://reactnavigation.org/) and [React Native Navigation](https://wix.github.io/react-native-navigation/#/). Despite the somewhat misleading name, they are both definitely React Native navigation libraries.

They both have more of less the same feature set - you can navigate between screens and stacks, add a bottom nav, create modals etc, so the choice really comes down to personal preference. React Native Navigation is the most similar with Facebook's own solution, and has historically had better performance. However, React Navigation has come a long way since it's initial release and should now be on par when it comes to performance.

For this workshop, we will be using React Navigation, because this is what is also bundle with Expo, and we want to keep the course content such that it could be followed with and without Expo.
