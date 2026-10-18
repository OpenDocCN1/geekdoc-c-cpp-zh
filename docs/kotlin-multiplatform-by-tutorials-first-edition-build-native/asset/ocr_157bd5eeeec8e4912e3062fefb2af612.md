**shared** module, check out the directory structure.

![](bbox=[0.321, 0.092, 0.681, 0.609])

Fig. 6.2 - Folder structure in Android Studio

There’s already a file called **Platform.kt** inside the project; or to be more exact, there are *four* of them — one for each platform you support, plus one. For making the expect/actual mechanism work, you’ll need to define the `expect` and `actual` entities in exactly the same package in each platform.

In the image above, the `expect` class for **Platform** is inside the **com.raywenderlich.organize** package under the **commonMain** directory. The `actual` implementations for iOS, Android and desktop are inside the same package under **iosMain**, **androidMain** and **desktopMain**, respectively.

# Creating the Platform class for the Common module

Open **Platform.kt** inside the **commonMain** folder. Replace the `expect` class definition with this: