application is now a bit more robust.

![](bbox=[0.163, 0.146, 0.836, 0.573])

+   13. In the **Left Operand** box, replace John with the number **10**. In the **Right Operand** box, type **Sharp**. Then select **Calculate**.
The try blocks the statements that parse both boxes, so the same exception handler handles user input errors in both boxes.
14. In the **Right Operand** box, replace Sharp with **20**, select the + **Addition** button, and then select **Calculate**.
The application now works as expected and displays the value 30 in the Result box.
15. In the **Left Operand** box, replace 10 with **John**, select the – **Subtraction** button, and then select **Calculate**.
Visual Studio drops into the debugger and reports a `FormatException` exception again. This time, the error has occurred in the `subtractValues` method, which