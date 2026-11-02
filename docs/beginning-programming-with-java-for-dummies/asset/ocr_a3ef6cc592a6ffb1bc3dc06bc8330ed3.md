# To wrap or not to wrap?

The last three statements in Listing 6-1 use a neat trick. You want the program to display just one line on the screen, but this line contains three different things:

+   - The line starts with We will bill $.
+   - The line continues with the amount variable's value.
+   - The line ends with to your credit card.

These are three separate things, so you put these things in three separate statements. The first two statements are calls to System.out.print. The last statement is a call to System.out.println.

Calls to System.out.print display text on part of a line and then leave the cursor at the end of the current line. After executing System.out.print, the cursor is still at the end of the same line, so the next System.out.whatever can continue printing on that same line. With several calls to print capped off by a single call to println, the result is just one nice-looking line of output, as Figure 6-5 illustrates.

Figure 6-5:
The roles played by System.out.print and System.out.println.

![](bbox=[0.18, 0.68, 0.78, 0.78])

A call to System.out.print writes some things and leaves the cursor sitting at the end of the line of output. A call to System.out.println writes things and then finishes the job by moving the cursor to the start of a brand-new line of output.