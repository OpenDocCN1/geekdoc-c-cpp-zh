# 52 Part I: Developer Tools

+   - The code is calculating the sum of the two numbers incorrectly in some situations.
- The problem seems to occur only when using decimal numbers.
- The error happens only when some decimal numbers are used, but not others. For example, 0.25 + 0.75 works as expected, but 4.2 + 2 does not. The reason that this happens is because the computer can't display fractional values (the numbers after the decimal point) if the values can't be represented as a non-repeating sequence in binary. If you want to know more about this topic (a word warning: it can get very messy), search for IEEE 794 on Google.com.

To you figure out where things are going wrong, Xcode includes a powerful debugger. With the debugger, you can follow along as your project's code executes and watch for any indication of a problem.

# Adding breakpoints

Before debugging this code, first set some breakpoints. Breakpoints are small markers that appear in the column to the left of the code. To insert a breakpoint, simply click in that leftmost column next to the line of code that you want to check with the debugger, as shown in Figure 3-9.

![](bbox=[0.227, 0.568, 0.853, 0.813])

Figure 3-9:
Click in the leftmost column of the editor to set a breakpoint.