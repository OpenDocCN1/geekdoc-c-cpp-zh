An action is a method that can handle events raised by views (for example, when a button is clicked) in the View window. An outlet, on the other hand, allows your code to programmatically reference a view on the View window.

With the File’s Owner item selected, choose the File ↔ Write Class File menu item. Interface Builder generates the code necessary to represent the outlets and actions that you have just added. Because the project template already includes class files that are used by the View Controller, you see the prompt as shown in Figure 3-14.

> **NOTE** You can also manually modify the View Controller files (the `.h` and `.m` files). But the Interface Builder has this nice little feature that helps you generate code for your outlets and actions.

![](bbox=[0.113, 0.391, 0.508, 0.527])

At this juncture, you have two options:

+   - Replace the existing class files in your project. Doing so overwrites all the changes that you might have made to your existing class files.
+   - Merge the newly generated code with the existing class files. I recommend this option because it allows you to selectively choose the statements to insert into your existing class files.

Click the Merge button. You should now see the window as shown in Figure 3-15, displaying the content of BasicViewController.h.