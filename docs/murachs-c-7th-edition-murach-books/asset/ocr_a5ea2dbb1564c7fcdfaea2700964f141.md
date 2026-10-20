# An introduction to exceptions

Before you learn how to handle exceptions, it’s helpful to know more about how exceptions work. In addition, it’s helpful to know how to display a dialog box that contains a message about an exception that has occurred. So that’s what you’ll learn in the two topics that follow.

It’s inevitable that your applications will encounter exceptions. For example, a user may enter data that’s not appropriate for the application. Then, if the application doesn’t check to be sure that the data is valid, the .NET runtime environment will *throw* an *exception* when it tries to work with that data. An exception is an object that’s created from the Exception class or one of its subclasses like the ones shown in figure 7-1. Exception objects represent errors that have occurred, and they contain information about those errors.

# How exceptions work

A well-coded application will *catch* specific exceptions that might be thrown and handle them. This is known as *exception handling*. Exception handling can be as simple as notifying users that they must enter valid data. However, for more serious exceptions, exception handling may involve notifying users that the application is being shut down, saving as much data as possible, cleaning up resources, and exiting the application as smoothly as possible.

When you’re testing an application, it’s common to encounter exceptions that haven’t been handled. In that case, Visual Studio will enter break mode and display an Exception Helper dialog box like the one shown in this figure. This dialog box includes the name of the class for the exception and a brief message that describes the cause of the exception.

All exceptions are *subclasses* of the Exception class. For example, the FormatException class is a subclass of the Exception class that represents a specific type of exception that occurs when a value of one data type can’t be converted to another data type. This exception can be thrown by the To() methods of the Convert class or the Parse() method of any class.

The ArithmeticException class is also a subclass of the Exception class. It represents an exception that occurs during an arithmetic, casting, or conversion operation. This class contains other subclasses, including the OverflowException and DivideByZeroException classes shown here. An overflow exception occurs when the result of an arithmetic, casting, or conversion operation is too large for the receiving variable. A divide-by-zero exception occurs if an application attempts to divide a number by zero.

For now, that’s all you need to know about the Exception hierarchy. As you progress through this book, though, you’ll learn about other types of exceptions. In section 5, for example, you’ll learn how to work with the exceptions that can occur when you’re working with databases. You’ll also learn more about subclasses and how they work in chapter 14.