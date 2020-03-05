---
path: '/lists-exercise-solution'
title: 'Lists Exercise Solution 👀'
order: 14
section: 'Basic components'
description: 'Solution to the lists exercise'
---

[🔗 Expo ed604b55573dbf95c2090ee34b6672fcc3fb05df](https://github.com/kadikraman/AwesomeProjectExpo/commit/ed604b55573dbf95c2090ee34b6672fcc3fb05df)

[🔗 RN 98c2e0bf744c42290c39b94afbed70db351e0de4](https://github.com/kadikraman/AwesomeProjectRN/commit/98c2e0bf744c42290c39b94afbed70db351e0de4)

In this solution we're removed the individual `ColorBox`es and rendered them all using a `FlatList`. Some things to note:

- since we no longer have a containing `View`, we not pass in the component styles into the `FlatList` component instead. Almost all native components in React Native can by styled using the style prop
- notice that the name of the palette scrolls with the colors. This is because we added it to FlatList using the `ListHeaderComponent` prop
- we've used a little calculation to adjust text colour for the background colour. There are better algorithms to do this, but this is definitely the shortest: `parseInt(props.hexCode.replace('#', ''), 16) > 0xffffff / 1.1`. Here we essentially get the lightest 10% of the background colors and display black text for these, and white for the rest.
