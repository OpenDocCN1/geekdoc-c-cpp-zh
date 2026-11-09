While handling an exception, a large amount of system resources and execution time are used. Therefore, you should avoid handling exceptions for predictable events. You can handle exceptions by using the following two statements:

+   - The try-catch-finally statement
+   - The throw statement

Let’s discuss these statements in detail.

# Using the try-catch-finally Statement

In the .NET Framework, exceptions are raised and handled at runtime. The .NET Framework provides a handler, called the **try-catch-finally** statement, to handle exceptions. When you use the try-catch-finally statement, the application is divided into different blocks of code. The code that is most likely to cause an exception is placed within the try block and the code that handles the exception is placed in the catch block. If an exception occurs, the catch block is executed and then the control is transferred to the finally block. Irrespective of the fact whether an exception occurs or not, the finally block is always executed. Multiple catch blocks are allowed for a single try block; however, there can be only one finally block for a try block.

If an exception is raised within the try statement, the control is transferred to the associated catch statement and afterwards to the finally statement, if it exists. In case the try statement does not throw any exception, the control is directly transferred to the finally statement, if it exists. A try statement without a catch or finally statement, results in a syntax error. A try statement must always be accompanied by either a catch or a finally statement. The syntax of a try-catch-finally statement is as follows:

```
```csharp
try
{
    // code which can cause exception
}
catch (exception-declaration)
{
    // the block of code that handles the exception
}
finally
{
    // the block of code to be executed whether the exception is raised or not
}
```
```

Let’s create an application to learn the use of the **try-catch-finally** statement by performing the following steps:

+   1. Start Visual Studio 2010.
+   2. Select **File→New→Project** from the menu bar. The **New Project** dialog box opens.
+   3. Select **Visual C#→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. Select **Windows Forms Application** in the right pane to create a Windows Forms application.
+   5. Enter the name of the application as **try_catch_finallyExample** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** box.
+   6. Click the **OK** button to close the **New Project** dialog box. The **try_catch_finallyExample** application is created (Fig.C#-7.19).
+   7. Select the Form1 and press the F4 key to open the Properties window of Form1 (Fig.C#-7.19).
+   8. Set the Text property of the Form1 form to Try Catch Finally, as shown in Fig.C#-7.19.