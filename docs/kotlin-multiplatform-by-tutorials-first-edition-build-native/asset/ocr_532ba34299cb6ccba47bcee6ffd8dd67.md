```
onAboutButtonClick: () -> Unit,
    ) {
        // ...
    }
```

Calling the `getViewModel()` extension function, which Koin provides, does all the creation and injection process.

Build and run the Android app. The app should behave as you’re familiar with — this time with DI, though.

![](bbox=[0.367, 0.253, 0.625, 0.658])



Koin is a Kotlin library. Lots of bridging occurs, should you want to use it with Swift and Objective-C files and classes. To make things easier, you’d better create some helper classes and functions.

Open **KoinIOS.kt** inside the **iosMain** directory.

Create a function inside an object for initializing Koin on iOS. Swift doesn’t bridge Kotlin functions with default parameters. This function is to compensate for that limitation.