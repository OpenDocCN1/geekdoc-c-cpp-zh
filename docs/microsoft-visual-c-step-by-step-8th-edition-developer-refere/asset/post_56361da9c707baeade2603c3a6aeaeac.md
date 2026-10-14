
+   2. Right-click anywhere in the first statement, and then click Run To Cursor.
+   3. When the form appears, type 999 in the number text box on the left, and then click Show Steps.
+   The program stops, and you are placed in Visual Studio 2015 debug mode.
+   A yellow arrow in the left margin of the Code and Text Editor window and yellow highlighting on the code indicates the current statement.
+   4. Display the Debug toolbar if it is not visible. (On the View menu, point to Toolbars, and then click Debug.)

## Note

The commands on the Debug toolbar are also available on the Debug menu displayed on the menu bar.

+   5. On the Debug toolbar, click the drop-down arrow, point to Add Or Remove Buttons, and then select Windows, as shown in the following image:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_167_0.png)

This action adds the Breakpoints Window button to the toolbar.

+   6. On the Debug toolbar, click the arrow that appears next to the Breakpoints Window button, and then click Locals.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_168_0.png)

The Locals window appears (if it wasn’t already open). This window displays the name, value, and type of the local variables in the current method, including the amount local variable. Notice that the value of amount is currently 0:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_169_0.png)

7. On the Debug toolbar, click the Step Into button.

The debugger runs the following statement:

Click here to view code image

```
int amount = int.Parse(number.Text);
```

The value of amount in the Locals window changes to 999, and the yellow arrow moves to the next statement.

8. Click Step Into again.

The debugger runs this statement:

```
steps.Text = "";
```

This statement does not affect the Locals window because steps is a control

on the form and not a local variable. The yellow arrow moves to the next statement.

## 9. Click Step Into.

The debugger runs the statement shown here:

```
string current = "";
```

The yellow arrow moves to the opening brace at the start of the do loop.

The do loop contains three local variables of its own: nextDigit, digitCode, and digit. Notice that these local variables appear in the Locals window, and the value of all three variables is initially set to 0.

## 10. Click Step Into.

The yellow arrow moves to the first statement within the do loop.

## 11. Click Step Into.

The debugger runs the following statement:

```
int nextDigit = amount % 8;
```

The value of nextDigit in the Locals window changes to 7. This is the remainder after dividing 999 by 8.

## 12. Click Step Into.

The debugger runs this statement:

```
amount /= 8;
```

The value of amount changes to 124 in the Locals window.

## 13. Click Step Into.

The debugger runs this statement:

Click here to view code image

```
int digitCode = '0' + nextDigit;
```

The value of digitCode in the Locals window changes to 55. This is the character code of the character “7” (48 + 7).

## 14. Click Step Into.

The debugger continues to this statement:

Click here to view code image

```
char digit = Convert.ToChar(digitCode);
```

The value of digit changes to “7” in the Locals window. The Locals window shows char values using both the underlying numeric value (in this case, 55) and also the character representation (“7”).

Note that in the Locals window, the value of the current variable is still “”.

## 15. Click Step Into.

The debugger runs the following statement:

```
current = current + digit;
```

The value of current changes to “7” in the Locals window.

## 16. Click Step Into.

The debugger runs the statement shown here:

Click here to view code image

```
steps.Text += current + "\n";
```

This statement displays the text “7” in the steps text box, followed by a newline character to cause subsequent output to be displayed on the next line in the text box. (The form is currently hidden behind Visual Studio, so you won’t be able to see it.) The cursor moves to the closing brace at the end of the do loop.

## 17. Click Step Into.

The yellow arrow moves to the while statement to evaluate whether the do loop has completed or whether it should continue for another iteration.

## 18. Click Step Into.

The debugger runs this statement:

```
while (amount != 0);
```

The value of amount is 124, the expression 124 != 0 evaluates to true, so the do loop performs another iteration. The yellow arrow jumps back to the opening brace at the start of the do loop.

## 19. Click Step Into.

The yellow arrow moves to the first statement within the do loop again.

## 20. Repeatedly click Step Into to step through the next three iterations of the do loop and watch how the values of the variables change in the Locals window.

## 21. At the end of the fourth iteration of the loop, the value of amount is 0 and the value of current is “1747”. The yellow arrow is on the while condition at the end of the do loop:

```
while (amount != 0);
```

Because the value of amount is now 0, the expression amount != 0 evaluates to false, and the do loop should terminate.

## 22. Click Step Into.

The debugger runs the following statement:

```
while (amount != 0);
```

As predicted, the do loop finishes, and the yellow arrow moves to the closing brace at the end of the showStepsClick method.

23. On the Debug menu, click Continue.

The form appears, displaying the four steps used to create the octal representation of 999: 7, 47, 747, and 1747.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_172_0.png)

24. Return to Visual Studio 2015. On the Debug menu, click Stop Debugging.

## Summary

In this chapter, you learned how to use the compound assignment operators to update numeric variables and append one string to another. You saw how to use while, for, and do statements to execute code repeatedly while some Boolean condition is true.

+   If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 6, “Managing errors and exceptions.”
+   If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference

| To | Do this |
|---|---|
| Add an amount to a variable | Use the compound addition operator. For example: `variable += amount;` |
| Subtract an amount from a variable | Use the compound subtraction operator. For example: `variable -= amount;` |
| Run one or more statements zero or more times while a condition is true | Use a *while* statement. For example: ``` int i = 0; while (i < 10) { Console.WriteLine(i); i++; } ``` Alternatively, use a *for* statement. For example: ``` for (int i = 0; i < 10; i++) { Console.WriteLine(i); } ``` |
| Repeatedly execute statements one or more times | Use a *do* statement. For example: ``` int i = 0; do { Console.WriteLine(i); i++; } while (i < 10); ``` |

## Chapter 6. Managing errors and exceptions

After completing this chapter, you will be able to:

- Handle exceptions by using the *try*, *catch*, and *finally* statements.
- Control integer overflow by using the *checked* and *unchecked* keywords.
- Raise exceptions from your own methods by using the *throw* keyword.
- Ensure that code always runs, even after an exception has occurred, by using a *finally* block.

You have now seen the core C# statements that you need to know to perform common tasks such as writing methods, declaring variables, using operators to create values, writing *if* and *switch* statements to run code selectively, and writing *while*, *for*, and *do* statements to run code repeatedly. However, the previous chapters haven’t considered the possibility (or probability) that things can go wrong.

It is very difficult to ensure that a piece of code always works as expected. Failures can occur for a large number of reasons, many of which are beyond your control as a programmer. Any applications that you write must be capable of detecting failures and handling them in a graceful manner, either by taking the appropriate corrective actions or, if that is not possible, by reporting the reasons for the failure in the clearest possible way to the user. In this final chapter of Part I, you’ll learn how C# uses exceptions to signal that an error has occurred and how to use the *try*, *catch*, and *finally* statements to catch and handle the errors that these exceptions represent.

By the end of this chapter, you’ll have a solid foundation in all the fundamental elements of C#, and you will build on this foundation in Part II.

## Coping with errors

It’s a fact of life that bad things sometimes happen. Tires are punctured, batteries run down, screwdrivers are never where you left them, and users of your applications behave in unpredictable ways. In the world of computers, hard disks become corrupt, other applications running on the same computer as your program run amok and use up all the available memory, wireless network connections disappear at the most awkward moment, and even natural phenomena such as a nearby lightning strike can have an impact if it causes a power outage or network failure. Errors can occur at almost any stage when a program runs, and many errors might not actually be the fault of your own application, so how do you detect them and attempt to recover?

Over the years, a number of mechanisms have evolved. A typical approach adopted by older systems such as UNIX involved arranging for the operating
