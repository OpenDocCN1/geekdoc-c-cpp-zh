+   - **Organize**, a multiplatform TODO app, in Section 2.
+   - **learn**, an RSS feed reader for raywenderlich.com articles, in Section 3.

They each had a customized version of a logger. The second challenge is to use the library that you created from the first challenge, on all three apps. Don’t forget to make the changes both at the business logic and UI levels.

# Challenge 3: Use the logger library in the shared-action module

At the beginning of this chapter, you successfully migrated the open links functions to Kotlin Multiplatform and created the **shared-action** module.

At the time, there was no logger class, so you used the `println` function as the module logger. With the recently created **shared-logger**, it’s now time to update **shared-action** and use your new library.

# Key points

+   - If the features you want to migrate to KMP have any platform-specific code, you need to write this specific logic for all the platforms your library will target.
+   - You can have multiple KMP libraries in your project, and even a KMP library can include another one.
+   - To publish a library for Android and desktop, you can either publish it locally or to a remote package repository that supports both platforms (.jar and .aar). In this book, you’ve seen how to use JitPack.
+   - For iOS, you’re creating a Swift package to share your library. Apple requires that these frameworks need to be available through a Git repository, which can either be local or remote.

# Where to go from here?

Congratulations! You’ve finished the last chapter of the book. Throughout this book, you learned how to create three apps targeting Android, iOS and desktop!

You started this journey by getting familiar with Jetpack Compose and Swift UI for UI development, and moved toward sharing your app’s business logic across these three platforms with Kotlin Multiplatform. You can now create an app from scratch and apply all of these new concepts, or migrate one that you’ve already written to KMP.