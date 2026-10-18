```
```gradle
dependencies {
    // 1
    implementation(project(":shared"))
    // 2
    implementation("com.google.android.material:material:1.4.0")
    implementation("androidx.appcompat:appcompat:1.3.1")

    implementation("androidx.constraintlayout:constraintlayout:2.1.1")
}
```
```

+   1. Android depends on the `shared` module (where all shared business logic will reside).
+   2. Android-specific libraries (Material Components & ConstraintLayout).

Next, the Android-specific settings:

```
```gradle
android {
    // 1
    compileSdk = 31
    defaultConfig {
        // 2
        applicationId = "com.raywenderlich.findtime.android"
        // 3
        minSdk = 21
        targetSdk = 31
        versionCode = 1
        versionName = "1.0"
    }
    // 4
    buildTypes {
        getByName("release") {
            isMinifyEnabled = false
        }
    }
}
```
```

+   1. **compileSdk** specifies the Android SDK version to compile against.
+   2. **applicationId** is the ID for the Android App. This has to be unique for every app on the Google Play store.
+   3. **minSdk** refers to the lowest Android version your app will run on, while **targetSdk** refers to the latest Android version you support. **versionCode** is the number you’ll use internally to differentiate between builds while **versionName** is the version that will be displayed on the Play Store.
+   4. Specify debug or release settings here. For the release version, this sets **isMinifyEnabled** to false, but you’ll probably want to set it to true when you’re ready to release.