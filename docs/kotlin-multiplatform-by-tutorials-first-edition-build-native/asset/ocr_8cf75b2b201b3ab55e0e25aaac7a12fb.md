From the project window, right-click on the top-level folder and choose New ▸ Directory. Name the directory shared-ui. Next, right-click on the shared-ui folder and choose New ▸ File. Name the file build.gradle.kts. Add the following:

```
import org.jetbrains.compose.compose

plugins {
    kotlin(multplatform)
    id(androidLib)
    id(composePlugin) version Versions.desktop_compose_plugin
}

android {
    // TODO: Add Android Info
}

kotlin {
    // TODO: Add Desktop Info
}
```

This adds the multiplatform, Android and Compose plugins. Now replace // TODO: Add Android Info with:

```
compileSdk = Versions.compile_sdk
sourceSets["main"].manifest.srcFile("src/androidMain/AndroidManifest.xml")
defaultConfig {
    minSdk = Versions.min_sdk
targetSdk = Versions.target_sdk
}
buildTypes {
    getByName("release") {
    isMinifyEnabled = false
    }
}
```

This is the minimum info needed for Android. For the desktop, replace // TODO: Add Desktop Info with:

```
// 1
android()
// 2
jvm("desktop") {
    compilations.all {
    kotlinOptions.jvmTarget = "11"
    }
}
sourceSets {
    // 3
    val commonMain by getting {
    dependencies {
    implementation(project(":shared"))
    }
}
```