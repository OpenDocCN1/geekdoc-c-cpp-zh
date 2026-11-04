# # IF-ELSE STATEMENTS

The previous example set shipping to a default value and then changed it if total was at least $100. Another way to think about this problem is to imagine taking one of two actions depending on total’s value. If total is less than $100, the program should set shipping to $5. Otherwise the program should set shipping to $0.

The if-else construct lets a program follow this approach, taking one of two actions depending on some condition.

The syntax for if-else is:

```
```
if (condition)
    statementsIfTrue;
else
    statementsIfFalse;
```
```

If *condition* is true, the first block *statementsIfTrue* executes. Otherwise (if *condition* is false) the second block *statementsIfFalse* executes.

Using the else keyword, the preceding code could be rewritten like this:

```
```
decimal shipping;
if (total < 100)
    shipping = 5M;      // Shipping is $5 if total < 100.
else
    shipping = 0M;      // Shipping is free if total >= 100.
```
```

You can use braces to make either the if or else part of the if-else statement execute more than one command.

# # CASCADING IF STATEMENTS

The if-else construct performs one of two actions depending on whether the condition is true or false. Sometimes a program needs to check several conditions to decide what to do.

For example, suppose an order entry program calculates shipping charges depending on the total purchase amount according to this schedule:

+   - If total < $20, shipping is $5.00.
+   - Otherwise, if total < $50, shipping is $7.50.
+   - Otherwise, if total < $75, shipping is $10.00.
+   - Otherwise, shipping is free.