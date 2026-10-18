Click **Finish** and wait for the project to synchronize.

As you can see, there’s a new **shared-ui** module in **learn**. Open the **settings.gradle.kts** file to confirm that it was added to your project.

Android Studio only has direct support for KMM (Kotlin Multiplatform Mobile). So, when you try to add a new module, and you’re targeting other platforms — like desktop apps — you’ll need to manually add these targets.

Open **shared-ui** and rename the **iosMain** folder to **desktopMain**.

Now, open the **shared-ui build.gradle.kts** and remove all the iOS references. Starting from the beginning of this file:

+   1. Moving towards the `kotlin` section, remove all the iOS targets:

```
```kotlin
listOf(
    iosX64(),
    iosArm64(),
    iosSimulatorArm64()
).forEach {
    it.binaries.framework {
        baseName = "shared-ui"
    }
}
```
```

+   2. Now on `sourceSets` delete all the `iOS*Main` and `iOS*Test` fields:

```
```kotlin
val iosX64Main by getting
val iosArm64Main by getting
val iosSimulatorArm64Main by getting
val iosMain by creating {
    dependsOn(commonMain)
    iosX64Main.dependsOn(this)
    iosArm64Main.dependsOn(this)
    iosSimulatorArm64Main.dependsOn(this)
}
val iosX64Test by getting
val iosArm64Test by getting
val iosSimulatorArm64Test by getting
val iosTest by creating {
    dependsOn(commonTest)
    iosX64Test.dependsOn(this)
    iosArm64Test.dependsOn(this)
    iosSimulatorArm64Test.dependsOn(this)
}
```
```

Now that there are no more iOS references, return to the `kotlin` section and under the `android()` target add:

```
```kotlin
jvm("desktop")
```
```