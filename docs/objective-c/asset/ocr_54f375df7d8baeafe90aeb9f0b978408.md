# Figure 2.1

The output of our application

![](bbox=[0.13, 0.142, 0.87, 0.535])

# Working with Statements and Expressions

All Objective-C programs are made up of statements and expressions. Statements are lines of code that exist strictly for the purposes of executing an action. Generally speaking, statements do not have return values, and so therefore do not change the state of the current line of execution except in ways that are side effects of calling the statement. In other words, the statement can branch into another line of code, and in that other line of code it can cause things to occur that have side effects (such as printing something to the console or displaying a dialog box), but it does not return a value to the current line of code that the statement is in.

Expressions, on the other hand, do return a value to the calling code, and therefore can be used to change program flow.

For the most part, the distinction between these two is minor enough to not be something to be concerned about. I use these two terms interchangeably.