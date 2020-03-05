---
path: '/pull-to-refresh'
title: 'Pull to refresh'
order: 25
section: 'Hooks and Network Requests'
description: 'We add a loading spinner for fetching and re-fetching'
---

Next we'd like to show the user when we're fetching data. Thankfully for us, native components have a scroll indicator built in! This comes in the form of [RefreshControl](https://reactnative.dev/docs/refreshcontrol) and you can use it with any _scrollable_ component: ScrollView, FlatList or SectionList.

All these scrollable components have a `refreshControl` props which should be used to pass in or customize the `RefreshControl` components. Let's import it and add it to our `FlatList`.

```js
import { RefreshControl } from 'react-native';

<FlatList
  refreshControl={<RefreshControl refreshing={true} onRefresh={() => {}} />}
/>;
```

Now you should see that the refreshControl is always visible! This is because we set the `refreshing` prop to always be true. Let's make this dynamic. First we'll need to create a new `useState` variable to hold the refreshing state:

```js
const [isRefreshing, setIsRefreshing] = useState(false);
```

Now we'll need a callback that

1. sets the refreshing state to `true`
2. re-fetches the data
3. sets the refreshing state back to `false`

```js
const handleRefresh = useCallback(async () => {
  setIsRefreshing(true);
  await handleFetchPalettes();
  setIsRefreshing(false);
});
```

Finally, let's pass the relevant variables into our `<RefreshControl>` component:

```js
<RefreshControl refreshing={isRefreshing} onRefresh={handleRefresh} />
```

In most cases, that's it! For me in this case I found that my API was too fast (what a problem to have, eh?) so I added a timeout to ensure the loading spinner is displayed for at least 1 second. It seems silly to make the app artificually _slower_, but sometimes it is a good practice from the UX point of view.

All you'll need to do it wrap the last `setIsRefreshing` in a `setTimeout`. The second argument for `setTimeout` is the length of the timeout in milliseconds:

```js
setTimeout(() => {
  setIsRefreshing(false);
}, 1000);
```

[🔗 RN 00b3292](https://github.com/kadikraman/AwesomeProjectRN/commit/00b329244904b84db00123c197304e30f32f70da)
