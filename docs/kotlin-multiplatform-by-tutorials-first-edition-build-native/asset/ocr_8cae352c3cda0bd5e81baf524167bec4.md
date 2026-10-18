```
```kotlin
actual val osName = when
(UIDevice.currentDevice.userInterfaceIdiom) {
    UIUserInterfaceIdiomPhone -> "iOS"
    UIUserInterfaceIdiomPad -> "iPadOS"
    else -> kotlin.native.Platform.osFamily.name
}

//2
actual val osVersion = UIDevice.currentDevice.systemVersion

//3
actual val deviceModel: String
    get() {
        memScoped {
            val systemInfo: utsname = alloc()
            uname(systemInfo.ptr)
            return NSString.stringWithCString(systemInfo.machine,
                encoding = NSUTF8StringEncoding)
                ?: "---"
        }
    }

//4
actual val cpuType = kotlin.native.Platform.cpuArchitecture.name

//5
actual val screen: ScreenInfo? = ScreenInfo()

//6
actual fun logSystemInfo() {
    NSLog(
        "($osName; $osVersion; $deviceModel;
${screen!!.width}x${screen!!.height}@${screen!!.density}x;
$cpuType)"
    )
}

actual class ScreenInfo actual constructor() {
    //7
    actual val width =
CGRectGetWidth(UIScreen.mainScreen.nativeBounds).toInt()
    actual val height =
CGRectGetHeight(UIScreen.mainScreen.nativeBounds).toInt()
    actual val density = UIScreen.mainScreen.scale.toInt()
}
```
```

+   1. There’s a class in `UIKit` called `UIDevice` from which you can query information about the `currentDevice`. In this code, you’re asking for the interface idiom to differentiate between iOS and iPadOS. The `UIUserInterfaceIdiom` enum has a couple more cases. For brevity, you used the Kotlin/Native `Platform` class to find information in the else block.
+   2. You can use `UIDevice` to get the OS version as well.
+   3. This is by far the clunkiest piece of code you’ll see in this book. But don’t worry: KMP isn’t usually like this. It’s here to show you where things can go wild. Objective-C at its core is C. There are some older APIs in Apple