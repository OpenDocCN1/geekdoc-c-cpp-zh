The form appears. You are now going to enter some text in the Left Operand box that will cause an exception. This operation will demonstrate the lack of robustness in the current version of the program.

4. In the Left Operand box, type John, and in the Right Operand box, type 2. Click the + Addition button, and then click Calculate.

This input triggers Windows default exception handling: the application simply terminates, and you are returned to the desktop!

Now that you have seen how the application behaves when an unhandled exception occurs, the next step is to make the application more robust by handling invalid input and preventing unhandled exceptions from arising.

# Write a try/catch statement block

+   1. Return to Visual Studio 2015.
+   2. On the Debug menu, click Start Debugging.
+   3. When the form appears, in the Left Operand box, type John, and in the Right Operand box, type 2. Click the + Addition button, and then click Calculate.

This input should cause the same exception that occurred in the previous exercise, except that now you are running in debug mode, so Visual Studio traps the exception and reports it.

Visual Studio displays your code and highlights the statement that caused the exception. It also displays a dialog box that describes the exception, which in this case is “Input string was not in a correct format.”