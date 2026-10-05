# Chapter 2    How to design a Windows Forms application    49

# How to adjust the tab order

+   - Tab order refers to the sequence in which the controls receive the focus when the user presses the Tab key. You should adjust the tab order so the Tab key moves the focus from one control to the next in a logical sequence.

+   - Each control has a TabIndex property that indicates the control's position in the tab order. You can change this property to change a control's tab order position.

+   - If you don't want a control to receive the focus when the user presses the Tab key, change that control's TabStop property to False.

+   - Label controls don't have a TabStop property so they can't receive the focus.

# How to set access keys

+   - Access keys are shortcut keys that you can use in combination with the Alt key to quickly move to individual controls on the form.

+   - You use the Text property to set the access key for a control by placing an ampersand immediately before the letter you want to use for the access key. For example, &Invoice sets the access key to I, but &Invoice sets the access key to n.

+   - Since the access keys aren't case sensitive, &N and &n set the same access key.

+   - When you set access keys, make sure to use a unique letter for each control. If you don't, the user may have to press the access key two or more times to select a control.

+   - You can't set the access key for a text box. However, if you set an access key for a label that immediately precedes the text box in the tab order, the access key will take the user to the text box.

# How to set the Enter and Esc keys

+   - The AcceptButton property of the form sets the button that will be activated if the user presses the Enter key.

+   - The CancelButton property of the form sets the button that will be activated if the user presses the Esc key. This property should usually be set to the Exit button.

+   - You set the AcceptButton or CancelButton values by choosing the button from a dropdown list that shows all of the buttons on the form. So be sure to create and name the buttons you want to use before you attempt to set these values.

# Another way to set the tab order

+   - In chapter 10, you'll learn how to use Tab Order to set the tab order of the controls on the form. If the form consists of more than a few controls, that is the best way to set that order.

![](bbox=[0.039, 0.943, 0.438, 0.96])