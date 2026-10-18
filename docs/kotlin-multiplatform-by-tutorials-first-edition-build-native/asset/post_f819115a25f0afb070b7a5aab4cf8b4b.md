
Add a feature to Organize that lets the user delete reminders individually. For the UI part, you may take advantage of swipe gestures on Android and iOS. On desktop, you can use a context menu that’s displayed when the user right-clicks on any reminder.

+   There are three major ways of persisting data on device: Key-Value storage, database and working directly with the file system.

+   Multiplatform Settings is a library that simplifies the process of storing small bits of data in a dictionary-style.

+   You can use databases to store structured data and access them in a certain way.

+   SQLDelight is a relationally based database that generates typesafe Kotlin API based on the SQL statements you write. When used in KMP, it uses SQLite under the hood.

+   Migrating databases is a delicate and important step when you want to change your database schema.

+   SQLDelight has an extension library that lets you observe database changes using Kotlin Flows.

This has been a long chapter. However, there remains lots of ground to cover.

Here are a couple of suggestions for you if you want to learn more:

+   Getting acquainted with SQL will let you write more performant queries.

+   Consulting the SQLDelight documentation, which is available here, will let you explore more of its features.

+   Testing is an essential aspect of development. As mentioned earlier, you can take advantage of in-memory databases in your tests. Both Multiplatform Settings and SQLDelight offer testing artifacts which you can exploit.

# 11 Serialization

Written by Carlos Mota

Great job on completing the first two sections of the book! You’re doing great. Now that you’re familiar with Kotlin Multiplatform, you have everything you need to tackle the challenges of this last section.

Here, you’ll start making a new app called **learn**. It’s built on top of the concepts you learned in the previous chapters, and it introduces a new set of concepts, too: serialization, networking and how to handle concurrency.

**learn** uses the raywenderlich.com RSS feeds to show the latest tutorials for Android, iOS, Unity and Flutter. You can add them to a read-it-later list, share them with a friend, search for a specific key, or just browse through everything the team has released. It will have the same look and feel you’re already used to from the raywenderlich.com website.

## The need for serialization

Your application can send or receive data from a third party, either a remote server or another application in the device. Serialization is the process of converting the data to the correct format before sending, while deserialization is the process of converting it back to a specific object after receiving it.

There are different types of serialization formats — for instance, JSON or byte streams. You’ll read more about this in Chapter 12, “Networking,” when covering network requests.

Android uses this concept to share data across activities, services or receivers — either in the same application or to third-party apps. The difference is that instead of relying on `Serializable` to send data from custom types, the OS requires you to implement `Parcelable` to send these objects.

## Project overview

To follow along with the code examples throughout this section, download the **starter** project and open **11-serialization/projects/starter** with Android Studio.

> **Note:** This project uses Jetpack Compose 1.2.0-alpha01 and Multiplatform

Compose 1.1.0 with Kotlin 1.6.10. To build and run the app successfully, use Android Studio Bumblebee 2021.1.1 Patch 2 or a newer version.

**Starter** has the skeleton of the app you’ll build, and **final** gives you something to compare your code to when you’re done.

After the project synchronizes, you’ll see a set of subfolders and other important files:

```
![](img/2f50555a40af4ea8c85f09e577f0c5b9_232_0.png)
Fig. 11.1 - Project view hierarchy
```

The next section explains the project tree hierarchy in detail. The folder names are self-explanatory and correspond to either the platform they are used for or the functionality itself. You’re welcome to skip it and go directly to the **Application features** section.

# Android app

Located inside **androidApp**, the Android app contains the Gradle configuration files, the app source code and its resources. It’s the same structure that you’re already used to from your Android apps, and you can use any library or component as you typically do:

+   - **components**: generic **Composable** functions that represent a specific purpose and are used in different screens.
+   - **ui**: contains all the UI. The sub packages correspond to specific screens (**bookmark, home, latest or search**), the navigation bar (**main**), the application design system (**theme**) or utility classes (**util**).
+   - **RWApplication.kt**: the **Application** class that initializes the **Context** needed by **SQLDelight**.

# Desktop application

The desktop application is similar to the Android app. The code was copied from one project to the other with just a couple of small changes — namely, on the libraries used that weren’t available for the **JVM target**:

+   - **Kamel**: Image loading library.
+   - **precompose**: A community library that lets you use **Jetpack Lifecycle**, **ViewModel**, **LiveData** and **Navigation** in a desktop application.

Although these libraries are available at the above links, they’re not updated to the latest versions of Kotlin or Compose. That’s why they’re included in this project. You can find more information about this in Appendix C.

To run the desktop application, go to the command line and in the project root folder, enter:

```
./gradlew desktopApp:run
```

After it finishes, a new window will open with the app. You’ll see a screen like this:

![](img/2f50555a40af4ea8c85f09e577f0c5b9_235_0.png)

Fig. 11.4 - Desktop starter project running. Empty screen with no data.

> **Note:** Use the mouse to change the window size.

# Shared module

This contains the entire business logic of **learn**. It’s the multiplatform code that’s shared across Android, iOS and desktop.

You’ll find:

+   - **androidMain**: Definition of Android platform-specific code.
+   - **androidTest**: Tests written for the platform-specific code mentioned above.
+   - **commonMain**: Contains the business logic that’s going to be shared across all the platforms targeted.
+   - **commonTest**: Contains all non-platform-specific tests created to validate if the business logic is working as expected.
+   - **iosMain**: Definition of iOS platform-specific code.
+   - **iostTest**: Tests written for the platform-specific code mentioned above.

When you open the shared module, you’ll see two things inside **commonMain**:

+   • **kotlin**: Where the application business logic is.

+   • **sqldelight**: Contains the SQL file that’s going to be used by **SQLDelight** to create the app’s database, along with the corresponding CRUD methods to interact with it.

This module follows the clean architecture paradigm, grouping files according to their responsibility in the business logic. Open the **kotlin** directory and you’ll see:

+   • **data**: Networking layer of the shared module. Fetches the RW feeds and defines the data model of each RSS entry.

+   • **domain**: Deserializes the response and creates a list of feeds that can later be consumed by the UI. Saves data into the database and defines the callbacks that are going to be used to notify when new data is available.

+   • **platform**: Declares which functionalities need to be implemented on each platform. It represents the platform-specific code of the app, and it’s where you’re going to find the **expect** keyword.

+   • **presentation**: This layer makes the bridge between the UI and the app logic.

+   • **ServiceLocator**: A singleton object that provides access to the different modules within the app. It’s also responsible to initialize all the Presenters along with the properties that they require.

In the next section, you’ll see what **learn** will look like after you implement all the required features.

Before starting to write code, have a look first at the app concept and its features:
