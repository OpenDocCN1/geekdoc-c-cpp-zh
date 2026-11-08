# Control Structures

The if, while, do, for, and switch statements are **control structures** and allow you to program branches and loops. With break and continue, you influence the flow of control structures: return also belongs to this family in the broadest sense. I would prefer not to mention goto (to find out why, see *Section 8.14*).

# 8.5  The “if” Statement

With the if statement, you program the *conditional execution* of statements. The simplest form executes the statement assigned to it only if a specified condition is met:

```
`if( Condition ) Statement`
```

You already know a bit about the statement part: here you should use a block with `{...}` so that you can group multiple statements and link them to the if. This is called the *then branch* of the if statement.

The *condition*, however, is still somewhat ominous. This must be an expression that evaluates to a truth value—that is, *true* or *false*. This applies to a specific group of expressions—namely, those that have the type bool.

More correctly, it must be possible to *convert* the expression to bool. This is a subtle but important difference that I explained in *Chapter 4, Section 4.4*. This simply means that you can also use a number like 0 or 42 and many other things directly as a condition in if. If you know how to handle it, `if(x-30)` and `if(cin>>val)` will come easily to you.

Here are a few conditions that can only be *true* or *false*:

+   - `number > 100`  
+     A simple arithmetic comparison that checks if *number* is greater than 100. You can also test for less than `<`, greater than or equal to `>=`, less than or equal to `<=`, equal to `==`, and not equal to `!=`.
+   - `number > 100 && number < 200`  
+     With the Boolean AND `&&`, you check if both expressions are true.
+   - `x < 0 || y < 0`  
+     The Boolean OR `||` fits when at least one condition should be met.
+   - `x == y+1`  
+     You can perform arithmetic calculations before a comparison.
+   - `(x > 0 || y > 0) && (maxx < 100 || maxx < 100)`  
+     Parenthesize complex expressions if necessary.
+   - `!(x < y)`  
+     With the operator `!` for *not*, you negate a Boolean expression; *true* becomes *false* and vice versa.