# Figure 12.10

When the user clicks the Help button on the title bar, the pointer changes to the question mark icon. Clicking on an object pops up Help text.

![](bbox=[0.18, 0.15, 0.55, 0.38])

# Figure 12.11

A popup Help topic pops up on top of the selected element.

![](bbox=[0.32, 0.35, 0.52, 0.42])

You can create popup Help by setting the form's HelpButton property to true and both the MaximizeBox and MinimizeBox properties to false. For each control that should display popup Help, you set the HelpString property to the text to show in a ToolTip-style box.

# Other Forms of User Assistance

Good programs provide assistance to the user. In this chapter, you learned about providing Help, context-sensitive Help, and popup Help. You also can provide helpful information using ToolTips and status bars. You might consider showing the formula for a calculation in a ToolTip as well as instructions for data entry. Instructions in status bars can be very useful and unobtrusive. It's a good idea to use the MouseOver event of controls to change the message in a status bar; then use the MouseOver event of the form to reset the status bar text.

# Feedback 12.1

+   1. Give the file type and purpose of each of the following file extensions.
+      a. .hhk
+      b. .hlp
+      c. .chm
+      d. .jpeg
+      e. .avi
+      f. .htm
+   2. List five types of user assistance that can be added to an application.