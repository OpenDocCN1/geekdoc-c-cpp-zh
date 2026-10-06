# Chapter 15 GUI Applications and Event-Driven Programming

+   * Line 15 multiplies the hours by payRate and assigns the result to the grossPay variable.
* Line 19 displays the gross pay. It does this by assigning the value of the grossPay variable to the grossPayLabel component's Text property. Notice that a function, realToString, is used to convert the grossPay variable to a string. This is necessary because many languages an error will occur if we try to assign a Real directly to a Text property. When we assign a value to a label component's Text property, that value will be displayed in the label.

To handle the event that occurs when the user clicks the exitButton, we would write the following event handler:

```
1 Module exitButtonClick()
2 Close
3 End Module
```

This event handler executes the Close statement. In pseudocode, the Close statement causes the window that is currently open to close. If the current window is the only one open, closing it causes the program to end.

![](bbox=[0.765, 0.415, 0.835, 0.455])

# In the Spotlight:
Designing an Event Handler

In the previous In Spotlight section, we designed the window shown in Figure 15-13 for Kathryn's test scoring averaging program.

**Figure 15-13** The window for the test scoring average

![](bbox=[0.218, 0.575, 0.765, 0.825])

Now, we will design the program's event handlers. When the user clicks the averageButton component, the program should calculate the average of the three test scores and display it in the averageLabel component. When the user clicks the exitButton component, the program should end. The pseudocode in Program 15-1 shows both event handlers.