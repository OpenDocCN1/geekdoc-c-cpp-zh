This time, you have chosen to run the method without stepping through it. The console window appears again, prompting you for the number of days.

+   14. In the console window, type **17**. Then press **Enter**.

Control returns to Visual Studio 2022. (You might need to bring Visual Studio to the foreground.) The yellow cursor moves to the third statement of the `run` method:

Click here to view code image

```
writeFee(calculateFee(dailyRate, noOfDays));
```

+   15. On the Debug toolbar, select **Step Into.**

The yellow cursor jumps to the expression that defines the body of the `calculateFee` method. This method is called first, before `writeFee`, because the value returned by this method is the parameter to `writeFee`.

+   16. On the Debug toolbar, select **Step Out.**

The `calculateFee` method call completes, and the yellow arrow jumps back to the third statement of the `run` method.

+   17. On the Debug toolbar, select **Step Into** again.

This time, the yellow arrow jumps to the statement that defines the body of the `writeFee` method.

+   18. Place the mouse over the `v` parameter in the method definition.

The value of `v`, `8925`, is displayed in a ScreenTip.

+   19. On the Debug toolbar, select **Step Out.**

The message “The consultant’s fee is: 9817.5” is displayed in the console window. (You might need to bring the console window to the foreground to display it if it’s hidden behind Visual Studio 2022.) The yellow arrow returns to the third statement in the `run` method.

+   20. On the Debug toolbar, select **Continue** to continue running the program without stopping at any subsequent statement.

> Tip