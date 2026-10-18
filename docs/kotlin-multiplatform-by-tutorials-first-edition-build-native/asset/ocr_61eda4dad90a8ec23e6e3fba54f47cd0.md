> Compose 1.1.0 with Kotlin 1.6.10. To build and run the app successfully, use Android Studio Bumblebee 2021.1.1 Patch 2 or a newer version.

**Starter** has the skeleton of the app you’ll build, and **final** gives you something to compare your code to when you’re done.

After the project synchronizes, you’ll see a set of subfolders and other important files:

![](bbox=[0.391, 0.235, 0.608, 0.489])

Fig. 11.1 - Project view hierarchy

The next section explains the project tree hierarchy in detail. The folder names are self-explanatory and correspond to either the platform they are used for or the functionality itself. You’re welcome to skip it and go directly to the **Application features** section.

# Android app

Located inside **androidApp**, the Android app contains the Gradle configuration files, the app source code and its resources. It’s the same structure that you’re already used to from your Android apps, and you can use any library or component as you typically do:

+   - **components**: generic **Composable** functions that represent a specific purpose and are used in different screens.
+   - **ui**: contains all the UI. The sub packages correspond to specific screens (**bookmark, home, latest or search**), the navigation bar (**main**), the application design system (**theme**) or utility classes (**util**).
+   - **RWApplication.kt**: the **Application** class that initializes the **Context** needed by **SQLDelight**.