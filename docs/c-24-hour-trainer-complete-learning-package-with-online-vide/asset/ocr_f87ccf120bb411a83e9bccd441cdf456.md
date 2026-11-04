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

+   1. If you run to the breakpoint and hover the mouse over the variables, you'll find that most of them make sense; the values numChicken = 9, priceChicken = 142.65, and so forth.

Step through the code, watching each line closely to see what's wrong.

+   1. While the program is stopped on the breakpoint, the variable priceTofu has value 0 because the code hasn't yet executed the line that sets its value. Press F10 to step over that line and you'll see that priceTofu is 13.95 as it should be. So far, you haven't found the bug.

If you continue stepping through the code, watching each line carefully, you'll eventually see the problem in this line:

```
tofuPriceTextBox.Text = priceChicken.ToString("C");
```

Here the code is making the tofu price TextBox display the value priceChicken!

> NOTE This is a fairly typical copy-and-paste error. The programmer wrote one line of code, copied and pasted it several times to perform similar tasks (displaying the values in the TextBoxes), but then didn't update each pasted line correctly.

Fix the error.

+   1. This bug is easy to fix. Simply change the offending line to this:
+   
+       tofuPriceTextBox.Text = priceTofu.ToString("C");

Run the program again and test it to make sure the change you made works. Try setting two of the quantities to 0 and the third to 1 to see if the program can correctly calculate the non-zero value.

+   1. If you run the program again, all should initially look fine. If you reproduce some calculations by hand, however, you may find a small discrepancy in the chicken prices.