---
title: "Async Storage"
date: 2022-10-19T19:10:31+05:30
draft: false
---

`AsyncStorage` is a module which allows you to persist data offline in React Native Apps.
It store data asynchronously in key-value fashion in serialized dictionary. It doesn't encrypt the data while storing. The `AsyncStorage` provides us JavaScript API. And each method in the API returns a Promise Object.

Since react native's AsyncStorage is depricated, we'll be using async-storage community package.

**Installation**

With npm:

```js
npm install @react-native-async-storage/async-storage
```

With yarn:

```js
yarn add @react-native-async-storage/async-storage
```

**Usage**

Here is a `Counter` Component which will increment when you press the button. The count will always start from 0 when you rebuild or restart the app.

```js
export const Counter = () => {
  const [count, setCount] = React.useState(0);

  return (
    <View>
      <Text>The button is clicked {count} times</Text>
      <Button
        title="Click me"
        onPress={() => setCount((newCount) => newCount + 1)}
      />
    </View>
  );
};
```

Not let's persist this count and everytime your application starts, it will start counting from the previous count.

**Importing**

```js
import AsyncStorage from "@react-native-async-storage/async-storage";
```

- Storing data  
  `setItem()` is used to store new data item. If the data item already exist, then it will modify the existing one.

Note : AsyncStorage can only store string data, which means you need to use `JSON.stringify()` when saving objects and similarly `JSON.parse()` while retrieving it.

```js
const storeCount = async (count) => {
  try {
    await AsyncStorage.setItem("count", count + "");
  } catch (error) {
    console.log(error);
  }
};
```

- Loading data  
  `getItem()` is used to load the data item's value. When the key exists, it returns a promise which resolves to stored values else it returns null.

```js
const getCount = async () => {
  try {
    const count = await AsyncStorage.getItem("count");
    return count === null ? 0 : parseInt(count, 10);
  } catch (error) {
    console.log(error);
  }
};
```

As you can see, here we converted the `count` to string and then again converted it back to integer while loading.

The Counter component now looks like this:

```js
export const Counter = () => {
  const [count, setCount] = React.useState(null);

  useEffect(() => {
    getCount().then((_count) => setCount(() => _count));
  }, []);

  useEffect(() => {
    storeCount(count);
  }, [count]);

  return (
    <View>
      <Text>The button is clicked {count} times</Text>
      <Button
        title="Click me"
        onPress={() => setCount((newCount) => newCount + 1)}
      />
    </View>
  );
};
```

As mentioned earlier, `getItem()` return promise. So we have resolved it and then called setCount.

**There are also other methods on AsyncStorage.**

1. mergeItem
2. removeItem
3. multiGet
4. multiSet
5. multiMerge
6. multiRemove
7. clear
8. useAsyncStorage
