
12. Run the application and perform a calculation. Then, change the value that's displayed in one of the text boxes. When you do that, the value that's displayed for the Future Value text box should be cleared.

13. When you're enhancements are working correctly, close the application.

# Exercise 6-2 Experiment with events

This exercise will give you a chance to experiment with events and the event wiring for the Future Value application.

# Generate and delete an event handler

- 1. Open the Future Value application that you enhanced in exercise 6-1.
- 2. In the Form Designer, double-click the form to generate the handler for the default event of a form, which is the Load event. Then, delete this event handler in the Code Editor, and try to build and run the application. This should lead to one build error.
- 3. Double-click on the error message, which will lead you to the event wiring for the event handler. Then, delete that wiring and try to build and run the application again. This time, it should work.

# Use a form event and two more control events

- 4. In the Form Designer, select the form, click the Events button in the Properties window, and double-click on the DoubleClick event to generate its event handler. Next, write the code for this handler so it sets the Text property for all four text boxes to an empty string. Then, test the application to make sure this works. (Be sure to double-click on the form, not on a control or the form's title bar.)
- 5. In the Form Designer, select the Monthly Investment text box, Next, select the MouseHover event, read its description, drop down its list, and select the ClearFuture event handler so it will be executed whenever the user lets mouse over this text box. Then, test the application to make sure this works.
- 6. In the Form Designer, select the Yearly Interest Rate box, and double-click on the DoubleClick event to generate its event handler. Next, write the code for this handler so it sets the value in the Yearly Interest Rate text box to 12. Then, test this enhancement.
- 7. Use your own imagination to work with other events. When you're through experimenting with events, close the application.

# How to handle exceptions and validate data

In the last two chapters, you learned how to code a Future Value application that calculates the future value of a series of monthly payments. However, if the user enters data that cannot be handled by this application, an exception will occur and the application will crash. In this chapter, you'll learn how to prevent that happening by handling any exceptions that occur and by validating data to prevent exceptions.

- An introduction to exceptions ................................................ 186
- How exceptions work ..................................................................... 188
- How to display a dialog box .................................................................. 188
- **How to use structured exception handling ................................. 190**
- How to catch an exception ....................................................................... 190
- How to use the properties and methods of an exception ................... 192
- How to catch specific types of exceptions ............................................... 194
- How to throw an exception ....................................................................... 196
- The Future Value application with exception handling ................ 198
- **How to validate data ................................................................. 200**
- How to validate a single entry ............................................................ 200
- How to use generic methods to validate an entry ................................ 202
- How to validate multiple entries ..................................................... 204
- **The Future Value application with data validation ............ 206**
- The dialog boxes ........................................................................ 206
- The code ..................................................................................... 206
- **Perspective ................................................................................... 210**

# An introduction to exceptions

Before you learn how to handle exceptions, it's helpful to know more about how exceptions work. In addition, it's helpful to know how to display a dialog box that contains a message about an exception that has occurred. So that's what you'll learn in the two topics that follow.

# How exceptions work

It's inevitable that your applications will encounter exceptions. For example, a user may enter data that's not appropriate for the application. Then, if the application doesn't check to be sure that the data is valid, the .NET runtime environment will throw an exception when it tries to work with that data. An exception is an object that's created from the Exception class or one of its subclasses shown in figure-7. Exception objects report what has occurred, and they contain information about those errors.

A well-coded application will catch any exceptions that might be thrown and handle them. Exception handling can be as simple as notifying users that they must enter valid data. However, for serious exceptions, exception handling may involve notifying users that the application is being shut down, saving as much data as possible, cleaning up resources, and executing the application smoothly as possible.

When you're testing an application, it's common to encounter exceptions that haven't been handled. In that case, Visual Studio will either break mode and display an Exception Dialog box like the one shown in this figure. This dialog box contains the name of the class for the exception, a brief message that describes the cause of the exception, and some troubleshooting tips to help you fix the problem that caused the exception to be thrown.

All exceptions are subclasses of the Exception class. For example, the FormatException is a subclass of the Exception class that represents a specific type of exception that occurs when a value of one data type can't be converted to another data type. This exception can be thrown by the To methods of the Convert class or the Parse method of any class.

The ArithmeticException is also a subclass of the Exception class. It represents an exception that occurs during an arithmetic, casting, or conversion operation. This class contains other subclasses, including the OverflowException and DivideByZeroException classes shown here. An overflow exception occurs when the result of an arithmetic, casting, or conversion operation is too large for the receiving variable. A divide-by-zero exception occurs if an application attempts to divide a number by zero.

For now, that's all you need to know about the Exception hierarchy. As you'll progress through this book, you'll learn all about other types of exceptions. In section 4, for example, you'll learn how to work with the exceptions that can occur when you're working with databases. You'll also learn more about subclasses and how they work in chapter 14.

# The dialog box for an unhandled exception

![](img/3148667e42d4db35b3d0857aaa1fa01_206_0.png)

# The Exception hierarchy for five common exceptions

![](img/3148667e42d4db35b3d0857aaa1fa01_206_1.png)

# Methods that might throw exceptions

| Class | Method | Exception |
| --- | --- | --- |
| Convert | ToDecimal(string) | FormatException |
| Convert | ToInt32(string) | FormatException |
| Decimal | Parse(string) | FormatException |
| DateTime | Parse(string) | FormatException |

7-1 How exceptions work

# How to display a dialog box

One way an application can communicate with its users is by displaying a dialog box that contains a message. In this chapter, dialog boxes are used to display messages about exceptions that have occurred. Keep in mind, however, dialog boxes can also be used for many other purposes.

To display a simple dialog box, you use the Show method of the MessageBox class as shown in figure 7-2. The syntax shown here lets you display a dialog box that contains a message, a title, and an OK button. For now, this simple dialog box is adequate.

In chapter 10, however, you'll learn how to use the MessageBox class to display more complex dialog boxes that include Yes, No, Cancel, Abort, Retry, and Ignore buttons, and you'll learn how to write code that checks which button the user selected. That way, you can handle an exception differently depending on how the user responds to the dialog box.
