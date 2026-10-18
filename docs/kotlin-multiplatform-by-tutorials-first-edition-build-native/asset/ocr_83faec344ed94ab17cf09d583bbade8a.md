Define all the plugin names by adding this code to the file:

```
```kotlin
const val androidPlugin = "android"
const val androidApp = "com.android.application"
const val androidLib = "com.android.library"
const val multiplatform = "multiplatform"
const val composePlugin = "org.jetbrains.compose"
const val cocopods = "native.cocoapods"
```
```

The code above defines regular Kotlin variables you can use throughout your Gradle scripts. These aren’t required, but they make it easier to add. Next, define the version numbers by adding the following code:

```
```kotlin
object Versions {
    // 1
    const val min_sdk = 24
    const val target_sdk = 31
    const val compile_sdk = 31

    // 2
    // Plugins
    const val kotlin = "1.6.10"
    const val kotlin_gradle_plugin = "1.6.10"
    const val android_gradle_plugin = "7.0.4"
    const val desktop_compose_plugin = "1.0.1"
    const val compose_compiler_version= "1.1.0-rc02"
    const val compose_version= "1.1.0-rc01"
                         // TODO: Add Other versions
}
// TODO: Add Deps
```
```

+   1. These define the SDK versions for Android. A min SDK version of 24 is needed for some of the libraries. You’ll notice these versions are consistent with the ones you saw earlier in the **build.gradle.kts** files.
+   
+   2. These define the versions for your plugins.

Notice the two plugins with the word `compose` in them. You’ll write your Android UI in Jetpack Compose and your desktop app in Desktop Compose. Now, define the version numbers for your libraries. Replace `// TODO: Add Other versions` with:

```
```kotlin
const val coroutines = "1.5.0-native-mt"
const val junit = "4.13.2"
const val material = "1.4.0"
const val kotlinXDateTime = "0.3.1"
const val activity_compose = "1.4.0"
const val napier = "2.1.0"
const val junit5 = "1.5.10"
const val frameworkName = "shared"
```
```