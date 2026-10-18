Organize: You go back to the tried-and-true copy and pasting!

The setup for the desktop app is a bit different from the Android app, though they both use Jetpack Compose. One difference is that you don’t use Jetpack Navigation Component on the desktop app. You also open the About Device page in a new window to be more in line with desktop conventions.

Except for a few nuances in design in the About page, like showing each data item in a Row instead of a Column, the code is the same. It’s there for you in the starter project. Open AboutView.kt , locate  //2  and  //3  and uncomment the code below them.

There are multiple ways to run the desktop app. You can open the Gradle menu on the side under desktopApp ▸ compose desktop and click run.

![](bbox=[0.25, 0.338, 0.747, 0.715])

The app runs, and it looks pretty much like the Android app.