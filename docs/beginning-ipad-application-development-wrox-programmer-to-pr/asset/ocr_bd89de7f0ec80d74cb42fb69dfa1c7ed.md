# THE WINDOW-BASED APPLICATION TEMPLATE

In this section, you discover another type of application template you can create using the iPhone SDK: the Window-based Application template. Unlike the View-based Application template, the Window-based Application template does not include a View Controller by default. Instead, it provides only the skeleton of an iPad application and leaves the rest to the developer — you need to add your own views and their respective View Controllers. Because of this, a Window-based Application presents a very good way for you to understand how View Controllers work and appreciate all the work needed to connect the View Controllers and XIB files. When you understand how View Controllers work, you will be on your way to creating more sophisticated applications.

To put first things first, execute the following Try it Out to write a Window-based Application and then progressively add a View Controller to it.

# TRY IT OUT  Creating a Window-based Application

*codefile windowBasedApp.zip available for download on Wrox.com*

+   1. Using Xcode, create a Window-based Application project and name it `windowBasedApp`. Observe the files created for this project type (see Figure 4-11). Apart from the usual supporting files, note that there is only one XIB file (`MainWindow.xib`) and two delegate files (`windowBasedAppAppDelegate.h` and `windowBasedAppAppDelegate.m`).
+   2. Press Command-R to test the application. An empty screen is displayed on the iPhone Simulator. This is because the Window-based Application template provides only the skeleton structure for a simple iPad application — just a window and the application delegate.
+   3. In Xcode, double-click `MainWindow.xib` to edit it in Interface Builder. Note that there are four items in the `MainWindow.xib` window (see Figure 4-12):
+      - File's Owner
+      - First Responder
+      - Window
+      - Window Based App App Delegate
+   4. From the Library window, drag and drop a View Controller item onto the `MainWindow.xib` window (see Figure 4-13). You will connect this View Controller item to a view that you will add to the project in the next step.

![](bbox=[0.75, 0.62, 0.93, 0.8])

![](bbox=[0.65, 0.72, 0.93, 0.9])