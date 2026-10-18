There is no best or worst way to do it.

Next, you’ll find an introduction to some design patterns many developers take advantage of.

# Model-View-Controller

The MVC pattern’s history goes back to the 1970s. Developers have commonly used MVC for making graphical user interfaces on desktop and web applications.

In the mobile world, Apple made MVC mainstream when it introduced the iPhone SDK in 2008. If you did iOS development before SwiftUI, you may have noticed that one of the base components was a `UIViewController`. It speaks for itself how Apple heavily invested in this pattern.

For long years before Google became opinionated about Android development patterns and architectures, developers used Model-View-Presenter, or **MVP**, which is a close deviation of MVC.

In MVC, you partition your code into three separate camps:

+   - **Model:** The central component of the pattern. It’s completely independent of the UI and handles the logic and rules of the application.
+   - **View:** Any representation of information, such as lists, grids, etc. This section is usually platform- and framework-dependent. You can use UIKit and SwiftUI on iOS and Views or Jetpack Compose on Android.
+   - **Controller:** Accepts input and converts it to commands for model or view. It also receives feedback from the model and reflects the changes to the view. It’s somehow the know-it-all of the pattern.

The diagram below shows the relationship between the different partitions:

![](bbox=[0.262, 0.724, 0.73, 0.932])