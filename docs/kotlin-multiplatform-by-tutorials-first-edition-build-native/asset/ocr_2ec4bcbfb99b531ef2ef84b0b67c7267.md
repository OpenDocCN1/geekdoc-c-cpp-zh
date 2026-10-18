# Kotlin Multiplatform by Tutorials Chapter 1: Introduction

![](bbox=[0.362, 0.064, 0.637, 0.487])

Your screen now shows the words Hello, Android and the Android version.

For iOS, open Platform.kt in shared/src/iosMain/kotlin/com/raywenderlich/findtime:

```
package com.raywenderlich.findtime

import platform.UIKit.UIDevice

actual class Platform actual constructor() {
    actual val platform: String = 
    UIDevice.currentDevice.systemName() + " " +
    UIDevice.currentDevice.systemVersion
}
```

Notice that this class is written in Kotlin but uses iOS platform code. Wow, you can write iOS code in Kotlin! When you build your project, the KMP plugin will compile this class into a framework. Open Xcode. From the File menu, choose Open and navigate to your project and into the iosApp folder. Select the workspace file (iosApp.xcworkspace). For the project to run without errors, you’ll need to build in Xcode. Select Product ▸ Build or press Command-B. Once the project is built, open ContentView.swift.