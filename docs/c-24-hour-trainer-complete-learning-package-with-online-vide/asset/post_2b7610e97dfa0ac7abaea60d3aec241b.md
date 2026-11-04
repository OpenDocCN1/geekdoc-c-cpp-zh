
Statement from the context menu. Alternatively, you can place the cursor on the line and press Ctrl+Shift+F10. When you let the program continue, it starts executing from this line.

Setting the next statement to execute is useful for replaying history to see where an error occurred, re-executing a line after you change a variable's value (described in the “Using the Immediate Window” section later in this lesson), or to jump forward to skip some code.

Note that you can jump to only certain lines of code. For example, you can't jump to a comment or other line of code that doesn't actually do anything (you can't set a breakpoint there either), you can't jump to a different method, you can't jump at all if an error has just occurred, you can't jump to a variable declaration unless it also initializes the variable, and so forth. C# does its best, but it has its limits.

## USING WATCHES

Sometimes you may want to check a variable's value frequently as you step through the code one line at a time. In that case, pausing between steps to hover over a variable could slow you down, particularly if you have a lot of code to step through.

To make monitoring a variable easier, the debugger provides watches. A watch displays a variable's value whenever the program stops.

To create a watch, break execution, right-click a variable, and select Add Watch from the context menu. The bottom of Figure 12-4 shows a watch set on the variable subtotal. Each time the program executes a line of code and stops, the watch updates to display the variable's current value.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_230_0.png)

FIGURE 12-4

The Watch window also highlights variables that have just changed in red. If you're tracking a lot of watches, this makes it easy to find the values that have just changed.

> NOTE The Locals window is similar to the Watch window except it shows the values of all of the local variables (and constants). This window is handy if you want to view many of those variables all at once. It also highlights recently changed values in red so you can see what's changing.

## USING THE IMMEDIATE WINDOW

While the program is stopped, the Immediate window lets you execute simple commands. The four most useful commands that this window supports let you view variable values, evaluate expressions, set variable values, and call methods.

> NOTE If you can't find the Immediate window, open the Debug menu, expand the Windows submenu, and select Immediate.

To view a variable's value, simply type the variable's name and press Enter. (Optionally, you can type a question mark in front if it makes you feel more like you're asking a question.)

The following text shows the Immediate window after I typed in the name of the variable subtotal and pressed Enter:

```
subtotal
19.95
```

To evaluate an expression, simply type in the expression and press Enter. You can include literal values, variables, properties, constants, and just about anything else that you can normally include inside an expression in the code.

The following text shows the Immediate window after I typed an expression and pressed Enter:

```
taxRate * subtotal
179.55
```

To set a variable's value, simply type the variable's name, an equals sign, and the value that you want to give it. The new value can be a literal value or it can be the result of an expression. After you press Enter, the Immediate window evaluates whatever is on the right of the equals sign, saves it in the variable, and then displays the variable's new value.

> NOTE The same technique lets you set new values for properties. For example, you can change a control's Location, Text, Visible, BackColor, and other properties on the fly.

The following text shows the Immediate window after I typed a statement to give the grandTotal variable a new value and pressed Enter:

```
grandTotal = subtotal + salesTax
199.50
```

Finally, to call a method, simply type the method call into the Immediate window and press Enter. Don't forget to add parentheses to the method call even if the method takes no parameters. The Immediate window calls the method and displays any returned result. If the method has no return value, the Immediate window displays “Expression has been evaluated and has no value.”

The following text shows the Immediate window after I executed the grandTotalTextBox's Clear method:

```
grandTotalTextBox.Clear()
Expression has been evaluated and has no value
```

> NOTE You must type commands in the Immediate window just as you would in the Code Editor. In particular, you must use the correct capitalization or the window will complain.

## TRY IT

If you look closely at Figure 12-5, you'll see that this program has a serious problem. One tofu dinner at $13.95 each probably shouldn't add up to $142.65. If you look a little more closely, you'll also see that the grand total doesn't add up properly.

In this Try It, you debug this program. You set breakpoints and use the debugger to evaluate variable values to figure out where the code is going wrong.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_232_0.png)

> NOTE The downloads for this chapter, which are available at www.wrox.com/go/csharp24hourtrainer2e, include buggy and debugged versions of the Try It and exercises. For example, the initial flawed version of the Try It is called “Try It 12” and the fixed version is called “Try It 12 Fixed.”

## Lesson Requirements

In this lesson, you:
- Use the debugger to fix this program. To follow along in the debugger, download this lesson's material from the book's website and open the “Try It 12” solution.
- Run the program and experiment with it for a bit to see what seems to work and what seems to be broken. This should give you an idea of where the problem may lie.
- Set a breakpoint in the code near where you think there might be a problem. In this case, the tofu dinner cost calculation is wrong so you might set a breakpoint on this line:
  `decimal priceTofu = tofuCost * numTofu;`
- Run the program so it stops at that breakpoint. Hover the mouse over different variables to see whether their values make sense.
- Step through the code, watching each line closely to see what's wrong.
- Fix the error.
- Run the program again and test it to make sure the change you made works. Try setting two of the quantities to 0 and the third to 1 to see if the program can correctly calculate the non-zero value.
- Repeat these steps until you can't find any more problems.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

## Step-by-Step

The first two lesson requirements for this Try It are fairly straightforward so they aren't repeated here. The following paragraphs discuss the solution to the mysterious problem, so if you want to try to debug the program yourself, do so before you read any further.

Ready? Let's go.

The following code shows how the program works. The bold line is where I set my breakpoint. If you stare at the code long enough, you'll probably find the bug, so don't look too closely or you'll spoil the surprise. Remember, the point is to practice using the debugger (which will be your only hope in more complicated programs), not to simply fix the program.

```
// Calculate the prices for each entree and the total price.
private void calculateButton_Click(object sender, EventArgs e)
{
    const decimal chickenCost = 15.85M;
    const decimal steakCost = 18.95M;
    const decimal tofuCost = 13.95M;

    // Get inputs.
    int numChicken = int.Parse(chickenQuantityTextBox.Text);
    int numSteak = int.Parse(steakQuantityTextBox.Text);
    int numTofu = int.Parse(tofuQuantityTextBox.Text);

    // Calculate results.
    decimal total = 0;

    decimal priceChicken = chickenCost * numChicken;
    total += priceChicken;
```

```
decimal priceSteak = steakCost * numSteak;
total += priceSteak;

decimal priceTofu = tofuCost * numTofu;
total += priceTofu;

// Display results.
chickenPriceTextBox.Text = priceChicken.ToString("C");
steakPriceTextBox.Text = priceSteak.ToString("C");
tofuPriceTextBox.Text = priceChicken.ToString("C");
totalTextBox.Text = total.ToString("C");
}
```

Run the program so it stops at that breakpoint. Hover the mouse over different variables to see whether they look like they make sense.

- If you run to the breakpoint and hover the mouse over the variables, you'll find that most of them make sense; the values numChicken = 9, priceChicken = 142.65, and so forth.

Step through the code, watching each line closely to see what's wrong.

- While the program is stopped on the breakpoint, the variable priceTofu has value 0 because the code hasn't yet executed the line that sets its value. Press F10 to step over that line and you'll see that priceTofu is 13.95 as it should be. So far, you haven't found the bug.

If you continue stepping through the code, watching each line carefully, you'll eventually see the problem in this line:

```
tofuPriceTextBox.Text = priceChicken.ToString("C");
```

Here the code is making the tofu price TextBox display the value priceChicken!

> NOTE This is a fairly typical copy-and-paste error. The programmer wrote one line of code, copied and pasted it several times to perform similar tasks (displaying the values in the TextBoxes), but then didn't update each pasted line correctly.

Fix the error.

- This bug is easy to fix. Simply change the offending line to this:
  
      tofuPriceTextBox.Text = priceTofu.ToString("C");

Run the program again and test it to make sure the change you made works. Try setting two of the quantities to 0 and the third to 1 to see if the program can correctly calculate the non-zero value.

- If you run the program again, all should initially look fine. If you reproduce some calculations by hand, however, you may find a small discrepancy in the chicken prices.
