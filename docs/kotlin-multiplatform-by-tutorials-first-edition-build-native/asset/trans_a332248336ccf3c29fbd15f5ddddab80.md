
There’s no `@StringRes` or `@DrawableRes`, since these annotations are Android-specific.

Additionally, to create the corresponding objects, you can do something similar to:

```kotlin
enum BottomNavigationScreens {
  ...

  case home(route: String, stringResId: Int, drawResId: Int)

  case search(route: String, stringResId: Int, drawResId: Int)
}
```

# Default arguments

Kotlin allows you to define default arguments for class properties or function arguments. For instance, you can define the default value for `platform` to always be `PLATFORM.ALL`. With this, you don’t necessarily need to define the `platform` value when creating a `RWContent` object. In these scenarios, the system will use the default one.

```kotlin
data class RWContent(
  val platform: PLATFORM = PLATFORM.ALL,
  val url: String,
  val image: String = ""
)
```

And to create this object:

```kotlin
val content = RWContent(
  url = "https://www.raywenderlich.com"
)
```

Now, if you print its content:

```kotlin
// > ALL
Logger.d(TAG, "platform=${content.platform}")
// > https://www.raywenderlich.com
Logger.d(TAG, "url=${content.url}")
// > ""
Logger.d(TAG, "image=${content.image}")
```

# Singletons

To create a singleton in Kotlin, you need to use the keyword `object`. The **ServiceLocator.kt** file — since it deals with object initialization — is one such example:

```kotlin
public object ServiceLocator
```

This guarantees that at all times, you’ll only have one reference to `ServiceLocator` throughout the scope of your app.

# Interfaces

Interfaces are similar to Swift protocols. They define a set of functions that any class or variable that uses them needs to declare.

Open **FeedData.kt** from **domain/cb** in the shared module:

```kotlin
public interface FeedData {

    public fun onNewDataAvailable(item: List<RWEntry>, platform: PLATFORM, e: Exception?)

    public fun onNewImageUrlAvailable(id: String, url: String, platform: PLATFORM, e: Exception?)

    public fun onMyGravatarData(item: GravatarEntry)
}
```

`FeedData` defines three different functions that will be called when there’s a network response. They’re declared on **FeedViewModel.kt** (inside **androidMain/home**) and used to notify the UI that there are new data available.

# Functions

Kotlin supports different types of functions:

# (non-line) functions

These functions are the ones that are more common to find in any source base. They’re quite similar to Swift `func`, but in Kotlin, this keyword loses a letter because it’s `fun`.:]

You can see different examples of functions in **FeedPresenter.kt**:

```kotlin
public fun fetchAllFeeds(cb: FeedData) {

    listener = cb
}
```

A function can also return an object. If you open **FeedAPI.kt** and look at `fetchRWEntry`, you can see that it’s returning a `HttpResponse` object. Moreover, since there’s only one instruction, you don’t need to add brackets and the return can be written on the same line. You just need to add the `=` sign:

```kotlin
public suspend fun fetchRWEntry(feedUrl: String): HttpResponse =
client.get(feedUrl)
```

# Lambda expressions

Lambda expressions allow you to execute specific code blocks as functions. They can receive parameters and even return a specific type of object. You can see two of them on `fetchFeed`: `onSuccess` and `onFailure` parameters on **FeedPresenter.kt**.

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

Both of these expressions receive an `it` parameter. In the first case, it’s a list of `RWEntry`, and in the second it’s an `Exception`. Alternatively, you could define this expression like the following to better identify what `it` really is:

```kotlin
onSuccess = { list ->
    listener?.onNewDataAvailable(list, platform, null)
}
```

# Higher-order functions

Higher-order functions support receiving a function as an argument.

A good example of this type of function is the `onSuccess` and `onFailure`

[PAGE 359]

You can find a comparison table between both languages in the [materials repository](materials repository).

# Where to go from here?

Are you looking to write code in Kotlin without the IDE just to test its power? JetBrains has the [Kotlin Playground](Kotlin Playground) that allows you to test some basic functions.

If you want to learn more about both languages, you’ve got the [Kotlin](Kotlin) and [Swift](Swift) Apprentice books that teach you everything you need to know about both languages in detail.

[PAGE 361]

# # Appendix B: Debugging Your Shared Code From Xcode

Written by Carlos Mota

Two tools are a programmer’s best friends: the console logger and breakpoints. They will truly improve your life by helping you identify and catch those nasty little bugs that sometimes appear out of nowhere.

You’ve used the logger throughout this book. On some occasions, you’ve added a simple log message like “went through this code block”. On other occasions, you’ve printed all the variables in a method. Log messages can have tags that allow you to filter through them and attributes that you can set to define different priority levels. This can help you easily understand where something went wrong.

Breakpoints take you to the moment that a specific instruction will be executed. You can see all the steps that lead to this stop and all that will succeed. Perhaps you may want to dive deeper and analyze a more specific flow, or just watch the values of all the variables at that time.

Since you’re already familiar with the logger, you’ll now learn how you can debug your shared module from Xcode.

# ## Debugging the shared module

Both Android Studio and Xcode have great debugging capabilities. The native code is simple to debug on both IDEs. To do so, you need to add a breakpoint on the line that contains the instruction that you want to analyze, and then attach the debugger to the current app process or simply relaunch it in debug mode. For both options, the app halts before executing that instruction.

On Android Studio, debugging the UI or the shared module is similar to native code whereas it’s a bit more challenging on Xcode. Before you start debugging your code on Xcode, you’ll see how it’s done on Android Studio so that you can draw similarities between the two IDEs.

# ## Debugging in Android Studio

The steps required to debug the shared module are the exact steps described earlier — but instead of adding a breakpoint on the Android app, you need to add it on the **shared** module.

[PAGE 362]

![](img/2f50555a40af4ea8c85f09e577f0c5b9_362_0.png)

Fig. B.1 - Android Studio Debugger Window

Before reaching a breakpoint, the app halts. You’ll see a screen similar to the one in the image. Here’s a step-by-step description of what you can do in debug mode:

+   1. Relaunches the app in debug mode.
+   2. Attaches the debugger to the app, without relaunching it.
+   3. Line breakpoint. Identifies where the app should suspend. This instruction will only be executed if you continue the debug process.
+   4. If you want to resume the app, you can click on this green arrow. The app will halt again at the next breakpoint.
+   5. Stops the app.
+   6. Shows the list of breakpoints that you’ve set.
+   7. Mutes breakpoints. While enabled, the app won’t suspend on any breakpoint.
+   8. Step over this instruction. Allows you to navigate to the next instruction inside the same scope.
+   9. Step into. Shows you the next method that’s going to be invoked. It doesn’t need to be at the same level as this line of code if the next instruction is a call to another class. This is contrary to step over, which would jump to the next instruction inside the same method.
+   0. Force step into the next instruction. This action is similar to the previous one. The difference is that if the next method that’s going to be invoked is
