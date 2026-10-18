```
```kotlin
android {
    publishLibraryVariants("release", "debug")
}
```
```

If you don’t define Android to publish its libraries, your project will use the one created for desktop by default. This is possible since JVM supports Android. However, this won’t work because the platform-specific code is entirely different on both platforms.

# Configuring a Multiplatform Swift package

You have different possibilities to generate a library. Since Apple has its own package manager — Swift Package Manager — and many libraries are now available through it, you’re going to use it in this chapter.

However, there’s no official plugin to generate a Swift Package from a KMM project. So, you’ll need to use the [Multiplatform Swift Package](#) plugin. In the **starter** project, you’ve got a **plugins**’ folder that contains an updated version of this library. Open the **settings.gradle.kts** file to include it in the project:

```
```kotlin
includeBuild("plugins/multiplatform-swiftpackage-m1_support")
```
```

> **Note:** This customized version of the plugin supports the Apple M1 architecture and uses the KMM **XCFramework** functions internally to generate the Frameworks.

Synchronize the project. Now, open the **build.gradle.kts** from **shared-action**, and add in the `plugins` section:

```
```kotlin
id("com.chromaticnoise.multiplatform-swiftpackage-m1-support")
```
```

You can define a couple of parameters to configure your Swift package. To accomplish this, add before the `kotlin` section:

```
```kotlin
//1
multiplatformSwiftPackage {
    //2
    xcframeworkName("SharedAction")
    //3
    swiftToolsVersion("5.3")
    //4
    targetPlatforms {
        iOS { v("13") }
```
```