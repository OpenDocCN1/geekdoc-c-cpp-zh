8. We can now build and run the project. As we input text to the TextBoxes and click the Button, these texts will be merged and added to the ListBox as shown in Figure 5.94.

> Please note that the texts written in TextBoxes are considered as texts (strings). Therefore we didn't need to do any conversion when we're writing these inputs in the ListBox.

![](bbox=[0.1, 0.32, 0.85, 0.7])

Figure 5.94. Using TextBoxes for text entering (new entries haven't been added to the ListBox yet)

# 5.19. ToolTip

ToolTips are used for adding tips (small information) about the controls on a form. When the mouse pointer is over the associated control, its ToolTip is activated and displays the related information.

The commonly used properties of ToolTips are as follows:

+   - **InitialDelay**: The time required for the mouse pointer stay on the control for the ToolTip to show the information.
+   - **ToolTipIcon**: Specifies the icon that will be shown with the information.
+   - **IsBalloon**: Sets if the information will be shown inside a balloon.