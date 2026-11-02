Populate the View window as shown in Figure 3-12. The following views are used:

+   - Label
+   - Text Field
+   - Round Rect Button

What your application will do is simple: When the user enters his or her name in the Text field and clicks the Round Rect button, the application displays an alert view showing the user's name.

# Creating Outlets and Actions

In order for your application to interact with views on the View window, you need a mechanism to reference your views on the window and at the same time provide methods to be invoked when some events happen on the window. In iPhone programming, these two mechanisms are known as outlets and actions, respectively.

In the BasicUIViewController.xib window (see Figure 3-13), select the File's Owner item and view its Identity Inspector window (choose Tools > Identity Inspector). Under the Class Actions section, click the plus (+) button to add an action named btnClicked:. Under the Class Outlets section, click the plus button to add an outlet named nameTextField. Set its Type to UITextField.

![](bbox=[0.677, 0.086, 0.916, 0.389])

![](bbox=[0.084, 0.537, 0.638, 0.945])