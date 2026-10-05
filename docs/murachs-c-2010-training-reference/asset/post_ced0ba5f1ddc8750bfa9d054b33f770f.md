
# The Help Viewer

Code and Text - Windows Internet Explorer

![](img/3148667e42d4db35b3d08576aaa1fa01_104_0.png)

## Description

- The Help Viewer lets you display content in your default web browser. You can display content that resides on your local system or in Microsoft's MSDN Online.

- You can display content-sensitive help in the Help Viewer by selecting an object in the Form Designer or positioning the insertion point in a keyword in the Code Editor and pressing F1. You can also display the Help Viewer by selecting the Help command from Visual Studio's Help menu.

- The Help Viewer is divided into two panes. The left pane displays the controls for performing a full-text search along with the table of contents. The right pane displays the last help topic that you accessed.

- To use full-text search, enter the text into the Search box and then click on the magnifying glass or press Enter. A list of topics that contain the search text will be displayed, and you can click on the topic you want to display.

- To use the table, click on a topic to display it in the right pane. Ancestors of the topic, topic peers, and peers of the parent topic are displayed in the left pane.

- You can use the Help Library Manager to choose local or online help, to check for updates, to install or remove local content. To display this manager, choose Manage Settings from Visual Studio's Help menu.

3-14 How to get help information

# How to run, test, and debug a project

After you enter the code for a project and correct any syntax errors that are detected as you enter this code, you can run the project. When the project runs, you can test it to make sure it works the way you want it to, and you can debug it to remove any errors you find.

# How to run a project

As you learned in chapter 1, you can run a project by clicking the Start Debugging button in the Standard toolbar, selecting the Start Debugging command from the Debug menu, or pressing the F5 key. This builds the project if it hasn't been built already and causes the project's form to be displayed, as shown in figure 3-15. When you close this form, the application ends. Then, you're returned to Visual Studio where you can continue working on your program.

You can also build a project without running it as described in this figure. In most cases, though, you'll run the project so you can test and debug it.

If errors are detected when you run a project, the errors are displayed in the Error List window, and you can use this window to identify and correct the errors. If it isn't already displayed, you can display this window by clicking on the Error List tab that usually displayed at the bottom of the window, or by using the View->Error List command. When you do that, you should realize that the errors will still be listed in the Error List window and highlighted in the Code Editor even after you've corrected them. The errors aren't cleared until you build the project again.

# The form that's displayed when you run the Invoice Total project

![](img/3148667e42d4db35b3d08576aaa1fa01_106_0.png)

## Description

- To run a project, click the Start Debugging button in the Standard toolbar, select the Debug->Start Debugging menu command, or press the F5 key. This causes Visual Studio to build the project and create an assembly. Then, if there are no build errors, the assembly is run so the project's form is displayed as shown above.
- If syntax errors are detected when a project is built, they're listed in the Error List window and the project does not run.
- To locate the statement that caused the error, you can double-click on the description in the Error List window. After you've corrected all the errors, run the project again to rebuild and clear the errors.
- You can build a project without running it by selecting the Build->Build Solution command.
- When you build a project for the first time, all of the components of the project are built. After that, only the components that have changed are rebuilt. To rebuild all components whether or not they changed, use the Build->Rebuild Solution command.

Figure 3-15 How to run a project

# How to test a project

When you test a project, you run it and make sure the application works correctly. As you test your project, you should try every possible combination of input data and user actions to be certain the project works correctly in every case. In other words, your goal is to make the project fail. Figure 3-16 provides an overview of the testing process for C# applications.

To start, you should test the user interface. Make sure that each control is sized and positioned properly, that there are no spelling errors in any of the controls or in the form's title bar, and that the navigation features such as the tab order and access keys work properly.

Next, subject your application to a carefully thought-out sequence of valid test data. Make sure you test every combination of data that the project will handle. If, for example, the project calculates the discounts at different values based on the value of the subtotal, subtotals fall within each range.

Finally, test the program to make sure that it properly handles invalid data entered by users. For example, type text information into text boxes that expect numeric data. Leave fields blank. Use negative numbers where they shouldn't be allowed. Remember that the goal of testing is to find all of the problems.

As you test your projects, you will encounter runtime errors. These errors, also known as exceptions, occur when C# encounters a problem that prevents a statement from being executed. If, for example, a user enters "ABC" into the Subtotal text box on the Invoice Total form, a runtime error will occur when the program tries to assign that value to a decimal variable.

When a runtime error occurs, Visual Studio breaks into the debugger and displays an Exception Assistant window like the one in this figure. Then, you can use the debugging tools you'll be introduced to in the next figure to debug the error.

Runtime errors, should only occur when you're testing a program. Before an application is put into production, it should be coded and tested so all all runtime errors are caught by the application and appropriate messages are displayed to the user. You'll learn how to do that in chapter 7 of this book.

# Chapter 3 How to code and test a Windows Forms application

# # The Exception Assistant that displayed when a runtime error

```csharp
private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal subtotal = Convert.ToDecimal(txttotal.Text);
    decimal discountPercent = 0;
    if
    {
        try
        Input string was not in a correct format.
        Make your method arguments are in the right format.
    }
    else
    {
        When converting a String to DateTime, parse the string to take the date by parsing each value into the DateTime object.
    }
    Get general help for this exception.
```

![](img/3148667e42d4db35b3d08576aaa1fa01_108_0.png)

# # How to test a project

- To test a project, run the project to make sure it works no matter what combination of valid or invalid data you enter or what sequence of controls you use.
- If a statement in your application can't be executed, a runtime error, or exception, occurs. Then, if the exception isn't handled by your application, the statement that caused the exception is highlighted and an Exception Assistant window like the one above is displayed. At that point, you need to debug the application.

Figure 3-16 How to test a project
