This screen shows all the articles that you’ve saved. Is the list getting big? Pick one and start reading it. Afterward, you can remove it from this list by clicking the three dots on the card and selecting **Remove from bookmarks**.

# Latest

This features a more graphical interface with the sections and covers of the latest articles. You can either scroll horizontally to see its content or vertically to switch across different topics.

# Search

There’s a lot of content that you can browse. Here, you can filter by a specific keyword and finally find that article you’ve been looking for.

Now that you’re familiar with the app and the project, it’s time to start learning how to implement these features.

# Adding serialization to your Gradle configuration

Kotlin doesn’t support serialization and deserialization directly at the language level. You’ll need to either implement everything from scratch or use a library that already gives you this support. Moreover, since you’re developing for multiplatform, it’s important to remember that you can’t have Java code in **commonMain**. Otherwise, the project won’t compile. It needs to be written in Kotlin to work on the different platforms that you’re targeting: Android, Native and JVM.

No, there’s no need to implement this support. It’s already available on **kotlinx.serialization**, a library created and maintained by JetBrains.

> **Note:** Read more about **kotlinx.serialization** from the official [documentation](https://).  
> Or, dive into the source code, available on its [official repository](https://).

Time to import this library into the app. Open Android Studio and wait for the project to finish synchronizing. In the project root folder, there’s a **build.gradle.kts** file; open it and add the following `classpath`:

```
```kotlin
classpath("org.jetbrains.kotlin:kotlin-serialization:1.6.10")
```
```

With this declaration, the build system knows where it should search and fetch