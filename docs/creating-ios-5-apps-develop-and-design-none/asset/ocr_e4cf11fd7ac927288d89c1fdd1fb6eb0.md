![](bbox=[0.054, 0.155, 0.263, 0.215])

**FIGURE 1.23** The Assistant Editor button

![](bbox=[0.286, 0.155, 0.916, 0.491])

**FIGURE 1.24** Side-by-side editing of the storyboard and the header file

# ADDING AN OUTLET

If we want to change the label’s text during runtime, we need a way to access it in our code. The easiest way is to add an outlet to the view’s controller. In the pre-Xcode 4.0 days, this meant jumping back and forth between Xcode and Interface Builder as we modified our code by hand. Now there’s a much simpler way.

First, we should probably collapse the scene list. Click the round, gray disclosure button in the lower-left corner of the Editor area. Next, click the Assistant Editor button (**Figure 1.23**).

This will display two Editor areas side by side. The leftmost area contains the selected file, while the rightmost contains a closely related file. For example, if you select the HWMainViewController.h header file, the right editor should display the HWMainViewController.m implementation file. In our case, the left editor shows the storyboard, while the right editor shows the controller’s header file (**Figure 1.24**).

Control-click the label and drag it to the header file. You will see a blue line stretching from the label to your cursor. Place the cursor just above the @end directive, as shown in Figure 1.25, and then release the mouse.

A pop-up dialog will now allow you to configure the outlet. Make sure the Connection setting is set to Outlet. In the Name field, enter label. The Type should be UILabel, and the Storage should be Strong (**Figure 1.26**). Click Connect to continue.