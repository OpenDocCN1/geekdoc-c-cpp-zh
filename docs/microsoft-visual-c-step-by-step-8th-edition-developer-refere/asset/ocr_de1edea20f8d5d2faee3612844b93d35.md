4. Press the Enter key to close the application and return to Visual Studio 2015.

In the next exercise, you’ll use the Visual Studio 2015 debugger to run your program in slow motion. You’ll see when each method is called (which is referred to as stepping into the method) and then see how each return statement transfers control back to the caller (also known as stepping out of the method). While you are stepping into and out of methods, you can use the tools on the Debug toolbar. However, the same commands are also available on the Debug menu when an application is running in debug mode.

# Step through the methods by using the Visual Studio 2015 debugger

+   1. In the Code and Text Editor window, find the run method.
+   2. Move the cursor to the first statement in the run method:

Click here to view code image

```
double dailyRate = readDouble("Enter your daily rate: ");
```

+   3. Right-click anywhere on this line, and then click Run To Cursor.

The program starts, runs until it reaches the first statement in the run method, and then pauses. A yellow arrow in the left margin of the Code and Text Editor window indicates the current statement, and the statement itself is highlighted with a yellow background.

![](bbox=[0.09, 0.51, 0.91, 0.905])

4. On the View menu, point to Toolbars, and then ensure that the Debug