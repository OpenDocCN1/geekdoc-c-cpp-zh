**COMMON MISTAKES** If you get an error stating that the page title is not valid, close your browser, return to VS, give the page a title, save your changes, and press F5 again.

Enter 5 in the first text box, 7 in the second, and then click the Calculate button. Instead of seeing the answer in your browser, you are now taken back to VS. If you're not taken back to VS directly, you may need to switch to it manually. You'll see the taskbar icon for VS flash to get your attention.

5. In VS, the line with the breakpoint is now highlighted in yellow. Additionally, you see a yellow arrow in the document margin to indicate this line of code is about to be executed. However, before it does, you get a chance to look at your controls, variables, and other elements that make up the execution environment. To see the values you entered in the TextBox controls, hover your mouse over the Text properties in the highlighted lines. You'll see, as shown in Figure 18-8, a small tooltip appear that displays the value you entered.

![](bbox=[0.12, 0.53, 0.45, 0.65])

# FIGURE 18-8

6. Hover your mouse over some of the variables in the code like result and value1. Note that you won't get a tooltip, because the code hasn't reached the point where these variables are declared. As far as the debugger is concerned, they don't exist.

7. To advance in the code, press F10. This steps over the selected line, executing it. Keep pressing F10 until the line that declares the value2 variable is highlighted. When you now hover your mouse over value1, the tooltip appears, indicating that value1 now contains the value 5.0.

8. Hover your mouse over the SelectedValue property in the Select Case (in VB.NET) or switch statement (in C#). Note that the tooltip shows you the value you selected in the drop-down list (the plus symbol). Even if this line of code hasn't been executed, the DropDownList control has been instantiated and its SelectedValue has been assigned a value earlier so you can look at it here.

9. Right-click the line that assigns the value to the ResultLabel control and choose Run to Cursor. This executes all code from the current breakpoint up to this line. Hover your mouse over the result variable (you may need to highlight the result variable first with your mouse if you are using VB.NET) and note that it displays the value 12.0, which is the outcome of the calculation, shown in Figure 18-9.

![](bbox=[0.68, 0.78, 0.9, 0.88])

# FIGURE 18-9

10. Finally, press F5. By pressing this key, the code continues until it finds the next breakpoint. Because you haven't defined another breakpoint in your code, the remainder of the code in the Click event handler is executed and the result is displayed in the page.