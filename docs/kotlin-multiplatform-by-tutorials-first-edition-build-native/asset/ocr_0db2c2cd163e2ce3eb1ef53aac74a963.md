# ## Migrating JVM-only libraries To Android

The accompanist libraries that the Android app uses are only being generated for this platform. Fortunately, the community once again comes to the rescue with a version that supports desktop. It was ported by the user Syer10, and you can find the repository on his GitHub.

The latest release now supports both Android and JVM, so you can easily add it to learn and share it across both platforms. Open the shared-ui build.gradle.kts and add to commonMain/dependencies:

```
api("ca.gosyer:accompanist-pager:0.20.1")
api("ca.gosyer:accompanist-pager-indicators:0.20.1")
```

Synchronize the project.

Although, you could use Google’s version in Android and Syer10 in desktop, since you’re sharing the UI between both platforms, you need to use the same one on both.

To give this support, both libraries build.gradle.kts files were updated with the Android target:

```
plugins {
    //1
    kotlin("multiplatform")
    id("org.jetbrains.compose") version "1.1.0"
    //2
    id("com.android.library")
}

kotlin {
    //3
    android {
    publishLibraryVariants("release", "debug")
    }

    //4
    jvm("desktop") {
    testRuns["test"].executionTask.configure {
    useJUnitPlatform()
    }
    }

    //5
    sourceSets {
    }
```