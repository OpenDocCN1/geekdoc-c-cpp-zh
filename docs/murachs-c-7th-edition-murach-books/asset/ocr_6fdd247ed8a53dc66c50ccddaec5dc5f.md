# Add an event handler for the TextChanged events

+   8. In the Form Designer, select the first text box. Then, click the Events button in the Properties window to display the Events list for that text box. Review the events that are available.

+   9. Enter “ClearFutureValue” to the right of the TextChanged event and press Enter. When you do, the Code Editor will open and an event handler named ClearFutureValue will be created. Enter a statement that clears the Future Value text box as shown in figure 6-12.

+   10. Open the frmFutureValue.Designer.cs file for the form, expand the Windows Form Designer generated code region if necessary, and locate the statements that set the properties of the Monthly Investment text box. At the end of those statements, you’ll find a statement that wires the TextChanged event of this control to the ClearFutureValue() event handler.

+   11. Return to the Form Designer and select the Yearly Interest Rate text box. Drop down the list for the TextChanged event of this control, and notice that the ClearFutureValue event handler is included in this list. Select this event handler to wire the event to it. Repeat this process for the Number of Years text box.

+   12. Run the application and perform a calculation. Then, change the value that’s displayed in one of the text boxes. When you do that, the value that’s displayed for the Future Value text box should be cleared.

+   13. When you’re sure the enhancements are working correctly, close the application.

# Exercise 6-2 Experiment with events

This exercise will give you a chance to experiment with events and the event wiring for the Future Value application.

# Generate and delete an event handler

+   1. Open the Future Value application that you enhanced in exercise 6-1.

+   2. In the Form Designer, double-click on the form to generate the handler for the default event of a form, which is the Load event. Then, delete this event handler in the Code Editor, and try to build and run the application. This should lead to one build error.

+   3. Double-click on the error message, which will lead you to the event wiring for the event handler. Then, delete that wiring, and try to build and run the application again. This time, it should work.

# Use a form event and two more control events

+   4. In the Form Designer, select the form, click the Events button in the Properties window, and double-click on the DoubleClick event to generate its event handler. Next, write the code for this handler so it sets the Text property for all four text boxes to an empty string. Then, test the application to make sure this works. (Be sure to double-click on the form, not on a control or the form’s title bar.)