12. Run the application and perform a calculation. Then, change the value that's displayed in one of the text boxes. When you do that, the value that's displayed for the Future Value text box should be cleared.

13. When you're the enhancements are working correctly, close the application.

# Exercise 6-2 Experiment with events

This exercise will give you a chance to experiment with events and the event wiring for the Future Value application.

# Generate and delete an event handler

+   1. Open the Future Value application that you enhanced in exercise 6-1.

+   2. In the Form Designer, double-click the form to generate the handler for the default event of a form, which is the Load event. Then, delete this event handler in the Code Editor, and try to build and run the application. This should lead to one build error.

+   3. Double-click on the error message, which will lead you to the event wiring for the event handler. Then, delete that wiring and try to build and run the application again. This time, it should work.

# Use a form event and two more control events

+   4. In the Form Designer, select the form, click the Events button in the Properties window, and double-click on the DoubleClick event to generate its event handler. Next, write the code for this handler so it sets the Text property for all four text boxes to an empty string. Then, test the application to make sure this works. (Be sure to double-click on the form, not on a control or the form's title bar.)

+   5. In the Form Designer, select the Monthly Investment text box, Next, select the MouseHover event, read its description, drop down its list, and select the ClearFuture event handler so it will be executed whenever the user lets mouse over this text box. Then, test the application to make sure this works.

+   6. In the Form Designer, select the Yearly Interest Rate box, and double-click on the DoubleClick event to generate its event handler. Next, write the code for this handler so it sets the value in the Yearly Interest Rate text box to 12. Then, test this enhancement.

+   7. Use your own imagination to work with other events. When you're through experimenting with events, close the application.