+   6. If it’s the same time zone as the current one, then you know it’s good.
+   7. Check if the hour is valid.
+   8. If, after going through every hour and it’s a good hour, add it to our list.
+   9. Return the list of hours.

Import the `min` and `max` methods. You’ve now written the business logic for the Time Finder app! Android, iOS, desktop and web platforms can all share it.

Build the app to make sure it still compiles. You can try to run both Android and iOS again. You’ll see the iOS build fail with the error shown below:

![](bbox=[0.143, 0.281, 0.858, 0.479])

Fig. 2.5 - Xcode build error details

Remember that you removed the `greet` method. How would you fix this?

# Challenge

The iOS app no longer works. Figure out how to find the problem, fix the error and get the iOS App working again.

# Key points

+   - Gradle is the build system for most of KMP projects.
+   - You write the Gradle build files in Kotlin.
+   - You use the **buildSrc** module to define variables and plugins.
+   - You write the Business logic in the **shared** module.
+   - The **kotlinx-datetime** library is a multiplatform library for handling dates and times.

# Where to go from here?