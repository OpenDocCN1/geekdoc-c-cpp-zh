The MsgBox keyword stops code execution and displays a string in a box that must be cleared before code execution continues. Here are the advantages of using the MsgBox statement:

+   - The MsgBox statement is easy to use and occupies only a single line of code.
+   - The MsgBox statement can output many types of data.
+   - The message box itself pops up right on the user interface, and you don't have to have the Immediate window open or flip to the Immediate window to view the message box.
+   - MsgBox halts code execution, and because you know where you've put the MsgBox statements, you know exactly where the code is executing.

There are also some problems associated with MsgBox statements:

+   - There is nothing about the MsgBox statement to prevent it from popping up in front of an end user, causing all kinds of confusion and other problems.

> CAUTION
> It's a good idea to remove all debugging statements from your code before shipping to end users. Search your code for MsgBox and Debug.Print to make sure all debugging statements have been removed.

+   - Message boxes are modal, which means you can't flip to the code editor window or Immediate window (discussed in the "Running code with the Immediate window" section) to examine the value of variables or examine the code underlying the application.
+   - It's difficult to get the text out of a message box. You can't copy the text or select parts of it. Other than reading the text in a message box, about the only other action you can do is print the screen.

# Compiler Directives

A refinement of the MsgBox technique is to use compiler directives to suppress the MsgBox statements, unless a special type of constant has been set in the code or within the Access environment. Examine the code in the following figure. Notice the #Const compiler directive above the MsgBox statement and the #If and #End If directives surrounding the MsgBox statement.