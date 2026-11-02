6. Click the first Tab Bar item labeled First (see Figure 8-4). In the Identify Inspector window, observe that this is a View Controller and that the implementing class is `FirstViewController`.

![](bbox=[0.08, 0.24, 0.6, 0.53])

FIGURE 8-4

7. Click the second Tab Bar item and view its Identity Inspector window. Notice that it is pointing to the base `UIViewController` class. Now, view its Attributes Inspector window (see Figure 8-5). Notice that in this case, it is loading its View window from another NIB file — `SecondView`.

> **NOTE** if you want users to interact with the UI in the second view, you should add a View Controller class to it so that you can connect outlets and actions to it. You will see how to do this shortly.