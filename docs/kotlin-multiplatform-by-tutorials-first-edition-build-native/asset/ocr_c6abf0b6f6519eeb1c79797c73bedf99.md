```
```kotlin
for (feed in content) {
    fetchFeed(feed.platform, feed.url)
}
```
```

A function can also return an object. If you open **FeedAPI.kt** and look at `fetchRWEntry`, you can see that it’s returning a `HttpResponse` object. Moreover, since there’s only one instruction, you don’t need to add brackets and the return can be written on the same line. You just need to add the `=` sign:

```
```kotlin
public suspend fun fetchRWEntry(feedUrl: String): HttpResponse =
client.get(feedUrl)
```
```

# Lambda expressions

Lambda expressions allow you to execute specific code blocks as functions. They can receive parameters and even return a specific type of object. You can see two of them on `fetchFeed`: `onSuccess` and `onFailure` parameters on **FeedPresenter.kt**.

```
```kotlin
private fun fetchFeed(platform: PLATFORM, feedUrl: String) {
    GlobalScope.apply {
        MainScope().launch {
            feed.invokeFetchRWEntry(
                platform = platform,
                feedUrl = feedUrl,
                onSuccess = { listener?.onNewDataAvailable(it, platform, null) },
                onFailure = { listener?.onNewDataAvailable(emptyList(), platform, it) }
            )
        }
    }
}
```
```

Both of these expressions receive an `it` parameter. In the first case, it’s a list of `RWEntry`, and in the second it’s an `Exception`. Alternatively, you could define this expression like the following to better identify what `it` really is:

```
```kotlin
onSuccess = { list ->
    listener?.onNewDataAvailable(list, platform, null)
}
```
```

# Higher-order functions

Higher-order functions support receiving a function as an argument.

A good example of this type of function is the `onSuccess` and `onFailure`