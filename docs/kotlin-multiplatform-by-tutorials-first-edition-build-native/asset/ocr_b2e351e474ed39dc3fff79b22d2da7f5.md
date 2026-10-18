```
remove these messages by adding the compiler argument: `-opt-in=kotlin.RequiresOptIn`.
```

Open the **shared build.gradle.kts** file and add the following code at the end of this file:

```
```kotlin
kotlin.sourceSets.all {
    languageSettings.optIn("kotlin.RequiresOptIn")
}
```
```

Depending on the data classes that you’re using, you might need to create an **expect/actual** class for other annotations. One of these examples is `@RawValue`, which is used along default serializers for custom types. You can follow the same approach used on **Parcelize** to achieve the same goal:

```
```kotlin
@OptIn(ExperimentalMultiplatform::class)
@OptionalExpectation
@Target(AnnotationTarget.TYPE)
@Retention(AnnotationRetention.BINARY)
expect annotation class RawValue()
```
```

With the expected declarations defined, go over to **androidMain** and create the corresponding **actual** implementation. It should be located in the same directory as the file you’ve just added on **commonMain**.

Navigate to the **platform** directory and create the corresponding **PlatformParcelable.kt** file. Open it and add:

```
```kotlin
package com.raywenderlich.learn.platform

actual typealias Parcelable = android.os.Parcelable
actual typealias Parcelize = kotlinx.android.parcel.Parcelize
```
```

Since `Parcelable` and `Parcelize` already exist on the Android platform, there’s no need to create them. Instead, use `typealias` to create a reference link between the expected class and the actual class itself. In other words, it’s as if you’re calling **android.os.Parcelable** or **kotlinx.android.parcel.Parcelize** directly.

> **Note:** Type aliases don’t create a new type of data, but instead create a link to an existing one. Get more information about Kotlin’s **typealias** directly from the [official documentation](...).