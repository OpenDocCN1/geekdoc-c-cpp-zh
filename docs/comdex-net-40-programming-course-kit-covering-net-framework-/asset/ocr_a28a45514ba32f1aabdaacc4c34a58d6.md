```
```csharp
int[] Numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
for (int i = 0; i < Numbers.Length; i++)
{
    if (Numbers[i] == 6)
        break;
    Console.WriteLine("Numbers[" + i + "] = " + Numbers[i]);
}
Console.ReadLine();
```
```

In the highlighted code of Listing 1.11, we first create an array of int type, Numbers, with the numbers from 1 to 10. After this, we use a for loop to display the array elements one by one. In the for loop, the local variable, i, is used as an index for the Numbers array to iterate through the array elements. The for loop contains an if statement, which checks whether the current array element has the value, 6. The condition in the if statement evaluates to false for the first five iterations of the for loop. Therefore, the for loop executes displaying the values of those five array elements. However, in the sixth iteration of the for loop, the condition in the if statement becomes true, resulting in the execution of the break statement. The break statement causes immediate termination of the for loop.

+   8. Press the F5 key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-1.27:

![](bbox=[0.399, 0.415, 0.624, 0.528])

# Using the continue Statement

The continue statement causes immediate termination of the current iteration of the loop in which it is used. It does not cause termination of the entire loop. The continue statement passes the control to the next iteration of the loop. If there are any statements that are written after the continue statement, then those statements are skipped.

The syntax of the continue statement is as follows:

```
```csharp
continue;
```
```

In the preceding syntax, the continue keyword indicates a continue statement.

Perform the following steps to understand the use of the continue statement:

+   1. Start Visual Studio 2010.
+   2. Select File→New→Project from the menu bar. The New Project dialog box opens.
+   3. Select Visual C#→Windows from the Installed Templates section in the left pane of the New Project dialog box.
+   4. Select Console Application from the middle pane to create a Console application.
+   5. Enter the name of the application as ContinueStatement (also available on the CD) in the Name text box and an appropriate location for the application in the Location box.
+   6. Click the OK button to close the New Project dialog box and create the ContinueStatement application.
+   7. Add the highlighted code snippet, shown in Listing 1.12, to the Program.cs file:

**Listing 1.12:** Showing the Code to Demonstrate the Use of the continue Statement

```
```csharp
using System;
```
```