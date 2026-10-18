
## 6. If it’s the same time zone as the current one, then you know it’s good.
## 7. Check if the hour is valid.
## 8. If, after going through every hour and it’s a good hour, add it to our list.
## 9. Return the list of hours.

Import the `min` and `max` methods. You’ve now written the business logic for the Time Finder app! Android, iOS, desktop and web platforms can all share it.

Build the app to make sure it still compiles. You can try to run both Android and iOS again. You’ll see the iOS build fail with the error shown below:

Fig. 2.5 - Xcode build error details

Remember that you removed the `greet` method. How would you fix this?

# Challenge

The iOS app no longer works. Figure out how to find the problem, fix the error and get the iOS App working again.

# Key points

- Gradle is the build system for most of KMP projects.
- You write the Gradle build files in Kotlin.
- You use the **buildSrc** module to define variables and plugins.
- You write the Business logic in the **shared** module.
- The **kotlinx-datetime** library is a multiplatform library for handling dates and times.

# Where to go from here?

In this chapter, you’ve learned how to setup your project with the **buildSrc** module to make changing versions easier. You also learned how to work with dates and times in the **shared** module, making it available for all platforms.

- Gradle: https://gradle.org/
- Kotlinx Datetime: https://github.com/Kotlin/kotlinx-datetime
- buildSrc: https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#:

In the next chapter, you’ll start building the UI for the Find Time project.

# Kotlin Multiplatform by Tutorials Chapter 3: Developing UI: Android Jetpack Compose

If you look at the source of `setContent`, you’ll see that it’s an extension method on `ComponentActivity` . The last parameter in this method is your UI. This method is of type `@Composable`, which is a special annotation that you’ll need to use on all of your Compose functions. A Compose function will look something like this:

```
@Composable
fun showName(text: String) {
    Text(text)
}
```

The most important part is the `@Composable` annotation. This tells JC this is a function that can be drawn on the screen. No `Composable` function returns a value. Importantly, you want most of your functions to be stateless. This means that you pass in the data you want to show, and the function doesn’t store that data. This makes the function very fast to draw. See the **Where to go from here** section at the end of this chapter to learn more about how Compose works.



You’re going to develop a multiplatform app that will allow the user to select

multiple time zones and find the best meeting times that work for all people in those time zones. Here’s what the first screen looks like:

Here, you see the local time zone, time and date. Two different time zones are below that: New York and London. Your user is trying to find a meeting time in all three locations.

> **Note**: This is just the raw time zone string code. If you’re interested, you can challenge yourself to replace the string codes with more readable strings.

When the user wants to add a time zone, they will tap the Floating Action Button (FAB) and a dialog will appear to allow them to select all the time zones they want:

Next up is the search screen, which allows the user to select the start and end times for their day and includes a search button to show the hours available.

## Themes

One of the first Compose functions you need to learn about is the theme. This is the color scheme you’ll use for your app. In Android, you would normally have a style.xml or theme.xml file with specifications for colors, fonts and other areas of UI styling. In Compose, you use a theme function. Since you have included the Material Compose library, you can use the MaterialTheme class as a starting point for setting colors, fonts and shapes. Compose can also tell you if the system is using the dark theme. Start by creating a new package in the androidApp module on the same level as MainActivity and name it theme.

Next, create a new file in that package named **Colors.kt**. Add the following:

```
import androidx.compose.ui.graphics.Color

val primaryColor = Color(0xFF1e88e5)
val primaryLightColor = Color(0xFF6ab7ff)
val primaryDarkColor = Color(0xFF005cb2)
val secondaryColor = Color(0xFF26a69a)
val secondaryLightColor = Color(0xFF64d8cb)
val secondaryDarkColor = Color(0xFF00766c)
val primaryTextColor = Color(0xFF000000)
val secondaryTextColor = Color(0xFF000000)
```

This defines some primary and secondary colors. You can see the colors in the left margin. Change them if you want a different color scheme. Next, right-click on the theme directory and create a new Kotlin file named **Typography.kt**. Add the following:

```
import androidx.compose.material.Typography
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui text.font.FontWeight
import androidx.compose.ui.unit.sp

// 1
val typography = Typography(
```
```

## Types

Before you get to the main screen, you’ll need a few types that will be used throughout the app. In the ui folder, create a new file named Types.kt. Add the following:

```
import androidx.compose.runtime.Composable

// 1
typealias OnAddType = (List<String>) -> Unit
// 2
typealias onDismissType = () -> Unit
// 3
typealias composeFun = @Composable () -> Unit
// 4
typealias topBarFun = @Composable (Int) -> Unit

// 5
@Composable
fun emptyComposable() {
}
```

1. Define an alias named OnAddType that takes a list of strings and doesn’t return anything.
2. Define an alias used when dismissing a dialog.
3. Define a composable function.
4. Define a function that takes an integer.
5. Define an empty composable function (as a default variable for the Top Bar).

Now that you have your colors and text styles set up, it’s time to create your first screen.

## Main screen

In the androidApp module in the ui folder, create a new Kotlin file named MainView.kt. You’ll start by creating some helper classes and variables. First, add the imports you’ll need (this saves some time importing):

```
import androidx.compose.foundation.layout.padding
import androidx.compose.material.BottomNavigation
import androidx.compose.material.BottomNavigationItem
import androidx.compose.material.FloatingActionButton
import androidx.compose.material.Icon
import androidx.compose.material.Scaffold
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Add
import androidx.compose.material.icons.filled.Language
import androidx.compose.material.icons.filled.Place
```
