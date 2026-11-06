![](bbox=[0.116, 0.093, 0.19, 0.175])

# Error-Prevention Tip 4.1

In a nested `if...else` statement, ensure that you test for all possible cases.

# 4.6.2 Dangling-`else` Problem

Throughout the text, we always enclose control statement bodies in braces (`{` and `}`). This avoids a logic error called the “dangling-`else`” problem. We investigate this problem in Exercises 4.23–4.25.

# 4.6.3 Blocks

The `if` statement normally expects only *one* statement in its body. To include *several* statements in the body of an `if` (or the body of an `else` for an `if...else` statement), enclose the statements in braces. As we’ve done throughout the text, it’s good practice to always use the braces. Statements contained in a pair of braces (such as the body of a control statement or function) form a *block*. A block can be placed anywhere in a function that a single statement can be placed.

The following example includes a block of *multiple* statements in the `else` part of an `if...else` statement: