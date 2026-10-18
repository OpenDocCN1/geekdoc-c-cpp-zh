Fig. 14.3 - Apple documentation for OpenURL function

In this image, you can find the `openURL` documentation:

+   1. These dots show you the path where **openURL** is located. You can see that **UIApplication** belongs to **UIKit** if you click on them. So, to access this function from **iosMain**, you’ll need to import:

```
```kotlin
import platform.UIKit.UIApplication
```
```

+   2. Open the **UIApplication** page. According to the documentation, the **UIApplication** is a singleton that you can access via `sharedApplication`. Therefore, to access **openURL**, you need to call:

```
```kotlin
UIApplication.sharedApplication.openURL(url)
```
```

+   3. This drop-down allows you to switch between Swift and Objective-C.

**Note:** You can see all the classes that exist inside **platform** if you go to JetBrains’ [kotlin-native repository](https://github.com/JetBrains/kotlin-native).

Now that you learned how to implement `openURL`, return to **PlatformAction.kt** from **shared-action/iosMain** and update the existing `openLink` function with:

```
```kotlin
public actual fun openLink(url: String) {
    val application = UIApplication.sharedApplication
    val nsurl = NSURL(string = url)
    if (!application.canOpenURL(nsurl)) {
        println("Unable to open url: $url")
        return
    }

    application.openURL(nsurl)
}
```
```

When prompted, import the following libraries:

```
```kotlin
import platform.Foundation.NSURL
import platform.UIKit.UIApplication
```
```

> **Note:** There’s currently an issue on the Android Studio for Mac M1 where the `platform` package seems to not be resolved. In other words, you might see the `platform` import along with the `UIApplication` and `NSURL` calls at red. If this is the case, don’t worry — you can compile the project without any problems.