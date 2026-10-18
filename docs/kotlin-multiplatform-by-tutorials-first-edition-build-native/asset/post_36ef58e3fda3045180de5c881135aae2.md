
takes a set of specifications and writes different code to implement those specifications. When testing, each team needs to make sure the logic they’ve implemented works the same as on the other platform. But with two different sets of code, how do they know that all the corner cases work the same way? With one codebase for business logic, both teams can review the code to make sure the logic matches the specifications and know it will work the same for both platforms. With one business logic code base, you can have either both teams work on it together or have one team specialize in writing business logic.

## Database

You can write the database layer using SQLite on mobile and desktop using the SQLDelight library. This library is a multiplatform package designed to run on all these platforms. Imagine having to write this set of code only once. Not only will you write only one set of lower-level SQL database insertions, deletions and updates, but your repository layer only needs to be written once. SQLDelight uses SQL statements to generate code for you. You only need to test once.

## UI

Since KMM doesn’t provide a UI layer, you can use whichever UI system you want. For iOS, developers are turning to **SwiftUI**: a nice, declarative UI toolkit that makes it easy to create beautiful UIs. Now that **Jetpack Compose** has been released as stable, Android developers can use it. Cross-platform desktop UIs have been neglected for quite a while. Swing has been a standard for some time, but it’s old and unmaintained. JetBrains hopes to replace it with **Compose for Desktop**. It uses a lot of Android’s Jetpack Compose underneath, with a layer of desktop code. Currently, there’s an issue with package names with Android using **androidx** and desktop using **org.jetbrains**. JetBrains hope to resolve this in the future.

## Is it Native?

One of the questions most often asked is: Does it use native controls? The answer is yes. Since KMP doesn’t provide any UI layer, all UI is drawn natively. On Android, that can be the built-in View system or the new Jetpack Compose library. On iOS, you can use the built-in native UI or the newer SwiftUI. On the desktop, you can use the older Java Swing or the newer Desktop Compose. For the Mac desktop, you can also use SwiftUI or AppKit. For Android, code is generated as Java class files, while iOS uses LLVM to produce native code and create an Xcode framework library.

## Current state of KMP

At the time of writing, KMP is currently in alpha, but production apps on both the Google and Apple stores already use it. Since there are multiple layers, here’s the current state of the platform as of the writing of this book:

| Component | Status |
|---|---|
| Kotlin/JVM | Stable |
| Kotlin/Native Runtime | Beta |
| KLib binaries | Alpha |
| expect/actual language feature | Beta |
| Multiplatform Gradle plugin | Beta |
| Kotlin/Native interop with C and Objective C | Beta |
| CocoaPods integration | Beta |
| Multiplatform IDE support | Alpha |
| KMM plugin for Android Studio | Experimental |

Fig. 1.1 — KMP Component Status

Since Android apps are built with Kotlin and have been for years, there are no compatibility issues. iOS and macOS apps interact with frameworks built with the KMM system. This will continue to evolve and improve but the feature is still in beta. Desktop apps can use the same shared code as the other platforms but use their own UI.

## Setting up your environment

You can use either IntelliJ or Android Studio to do KMP work. In this book, you’ll use Android Studio because it seems to work better with mobile platforms at the time of writing.

## Download Android Studio

Go to https://developer.android.com/studio and download Android Studio Bumblebee edition or later. Once installed, go to Android Studio’s preferences and then to plugins. Search for **multiplatform** and install the **Kotlin Multiplatform Mobile** plugin:

## Install CocoaPods

CocoaPods is a dependency manager for iOS. Since CocoaPods has been around for a long time, it’s easy to use in Xcode and easy to add dependencies.

Run the following command in Terminal on your Mac:

```
sudo gem install cocoapods
```

The command above installs cocoapods using the default Ruby installation available on macOS.

## Creating your first project

It’s time to create your first project! In Android Studio, open the File menu and choose New ▸ New Project.

In the New Project window, scroll down to the last entry and choose Kotlin Multiplatform App. If you don’t see this, make sure you installed the KMM plugin. Also, make sure to restart Android Studio after installing the plugin. Click Next.

In the next dialog, enter the name **Find Time** and a package name of **com.raywenderlich.findtime** or your own package name. Choose the directory you want to store the project and press **Next**.

# Kotlin Multiplatform keywords

Now that you have the project created, you need to know about two new keywords that were added to the Kotlin language to support KMP: **expect** and **actual**. These let you create functions or variables in the shared module using the **expect** keyword. Those functions or variables aren’t defined in the **commonMain** folder, but are _expected_ in each multiplatform module — like **androidMain** or **iosMain**. If you open the shared folder, you’ll see:

Here, you can see folders for Android, common and iOS. You’ll add the shared classes and code to **commonMain/kotlin**. If you need to write code that is platform specific, you’ll write an **expect** function or variable in the common folder and the **actual** code in both the Android and iOS folders. Open the **commonMain** folder and open **Platform.kt**.

```
package com.raywenderlich.findtime
expect class Platform() {
    val platform: String
}
```
