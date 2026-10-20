# How to debug runtime errors

When a runtime error occurs, Visual Studio enters *break mode*. In that mode, Visual Studio displays the Code Editor and highlights the statement that couldn’t be executed, displays the Debug toolbar, and displays an Exception Helper window like the one shown in figure 3-14. This is designed to help you find the cause of the exception (the *bug*), and to *debug* the application by preventing the exception from occurring again or by handling the exception.

Often, you can figure out what caused the problem just by knowing what statement couldn’t be executed or by reading the message displayed by the Exception Helper. But sometimes, it helps to find out what the current values in some of the variables or properties in the program are.

To do that, you can place the mouse pointer over a variable or property in the code to display a *data tip* as shown in figure 3-15. This tip displays the current value of the variable or property. You can do this with the Exception Helper still open, or you can click on its Close button to close it. Either way, the application is still in break mode. In this figure, the data tip for the Text property of the txtSubtotal control is “$100”, which shows that the user didn’t enter valid numeric data.

Once you find the cause of a bug, you can correct it. Sometimes, you can do that in break mode and continue running the application. Often, though, you’ll exit from break mode before fixing the code. To exit, you can click the Stop Debugging button in the Debug toolbar. Then, you can correct the code and test the application again.

For now, don’t worry if you don’t know how to correct the problem in this example. Instead, you can assume that the user will enter valid data. In chapter 7, though, you’ll learn how to catch exceptions and validate all user entries for an application because that’s what a professional application has to do. And in chapter 11, you’ll learn a lot more about debugging.