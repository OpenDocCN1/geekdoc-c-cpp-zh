```
}
}
```

This is important because **MainActivity.kt** is observing all the changes on `items`. Open this class and you’ll see that `items` contains the data required to populate the app screens.

Build and run the Android application. You’ll see a screen similar to this one:

![](bbox=[0.392, 0.224, 0.607, 0.568])

Navigate to the **desktopApp** project and add the same logic. On **FeedViewModel.kt**, find the `fetchAllFeeds` function and add:

```
presenter.fetchAllFeeds(this)
```

**Main.kt** calls this function to fetch all the available feeds. When they’re ready, `onNewDataAvailable` is called with all the items. Update this function to:

```
override fun onNewDataAvailable(newItems: List<RWEntry>, platform: PLATFORM, exception: Exception?) {
    Logger.d(TAG, "onNewDataAvailable | platform=$platform items=${items.size}")
    viewModelScope.launch {
        _items[platform] = items
    }
}
```

Now that the desktop app is ready, enter the compilation and run command at