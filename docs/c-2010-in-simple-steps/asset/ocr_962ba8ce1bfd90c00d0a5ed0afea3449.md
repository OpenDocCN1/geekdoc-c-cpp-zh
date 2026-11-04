+   - **Iteration statement:** Allows you to repeatedly perform a specified task(s) until certain condition is reached. The examples of iteration statements are **for**, **while**, **do...while**, and **foreach** loops.
+   - **Jump statement:** Transfers the program control to a different section of code. The **break**, **continue**, **goto**, **default**, and **return** statements are examples of the jump statements.

**Note**
You learn about the selection statements, iteration statements, and jump statements in detail later in this chapter.

Let's now learn about the selection statements.

# ### Working with Selection Statements

In C#, the statements that cause the flow of a program to change based on a certain condition are known as selection statements. The program control checks a condition before executing the code inside the selection statement. The selection statement causes the program control to adopt a specific flow of execution based on whether or not a certain condition is true. C# supports the following two types of selection statements:

+   - **if statement:** Allows you to test whether or not a certain condition is true. If the condition is true, the program control is transferred to the block of code that is inside the **if** statement; otherwise, the program control is transferred to another block of code.
+   - **switch statement:** Allows you to compare an expression with different values.

Now, let's discuss each of these selection statements in detail.

# ## The if Statement

One of the most important and commonly used selection statement in C# is the **if** statement. The **if** statement evaluates a specified condition or a set of conditions to true or false. If the condition is true, the program control enters the **if** block and executes all the statements and instructions inside the **if** block. The syntax of the **if** statement is as follows:

```
```csharp
if condition { // condition
    //statement
}
```
```

In the preceding syntax, if the condition inside the **if** block is evaluated to true, then the program control is transferred to the statements inside the **if** block and executes the statements.
Now, let's create a console application named **If Example** to learn how to use the **if** statement. Perform the following steps to create the **If Example** application:

+   1. Click Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010 to open the Visual Studio 2010 integrated development environment (IDE).
+   2. Select File→New→Project from the menu bar.
+      The New Project dialog box appears.
+   3. Select Visual C# from the Installed Templates pane and then select the Console Application option from the middle pane of the New Project dialog box.
+   4. Enter If Example in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have selected the location, D:\C#2010 Applications.
+   5. Click the OK button. The If Example application is created, as shown in Fig.C#-3.1: