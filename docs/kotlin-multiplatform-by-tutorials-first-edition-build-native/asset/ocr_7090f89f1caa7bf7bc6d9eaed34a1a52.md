This `InvalidMutabilityException` means you’re accessing an object that belongs to another thread, which is currently not possible. Confirm if you’re using the **Dispatchers.Main** or the **ioDispatcher** that you’ve created previously to access that object.

If you’re still running into problems:

+   - Delete the **build** folder in the root directory of the project.
+   - Delete the **build** folder in the **shared** directory in the root directory of the project.

# Frozen state

In some instances, you might need to freeze your objects when running your iOS app to avoid having the error mentioned above. Once `freeze()` is called over an object, it becomes immutable. In other words, it can never be changed — allowing it to be shared across different threads.

Another advantage of using the **kotlinx.coroutines** library is that this logic is already built into the library, in its latest versions, so you shouldn’t need to do anything from your side.

# Working with kotlinx.coroutines

On the app, go to the **latest** screen. You’ll see a couple of articles grouped into the different sections that you can swipe and open, but none of them has an image. It’s time to change this!

# Creating a suspend function

Start by opening the **FeedAPI.kt** file from **data/commonMain** in the **shared** module. After the `fetchRWEntry`, add:

```
public suspend fun fetchImageUrlFromLink(link: String):
HttpResponse = client.get(link) {
    header(HttpHeaders.Accept, "text/html")
}
```

This `fetchImageUrlFromLink` receives the link from an article and returns the page source code as the `HttpResponse`. It needs to be set as a `suspend`, so the current thread won’t block while it’s waiting for the server response.

> **Note:** You need to set the `Accept` header in this request otherwise the server