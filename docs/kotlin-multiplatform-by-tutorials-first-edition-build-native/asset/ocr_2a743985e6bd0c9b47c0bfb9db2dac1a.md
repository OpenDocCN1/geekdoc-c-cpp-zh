```
```bash
cd "$SRCROOT/.."
./gradlew :shared:embedAndSignAppleFrameworkForXcode
```
```

This task automatically compiles the **SharedKit** framework and adds it to your project when necessary.

After the project is synchronized, compile and run the app. You’ll see a screen like this:

![](bbox=[0.393, 0.246, 0.616, 0.551])

Fig. 11.3 - iOS starter project running. Empty screen with no data.

# Desktop application

The desktop application is similar to the Android app. The code was copied from one project to the other with just a couple of small changes — namely, on the libraries used that weren’t available for the **JVM target**:

+   - **Kamel**: Image loading library.
+   - **precompose**: A community library that lets you use **Jetpack Lifecycle**, **ViewModel**, **LiveData** and **Navigation** in a desktop application.

Although these libraries are available at the above links, they’re not updated to the latest versions of Kotlin or Compose. That’s why they’re included in this project. You can find more information about this in Appendix C.

To run the desktop application, go to the command line and in the project root folder, enter: