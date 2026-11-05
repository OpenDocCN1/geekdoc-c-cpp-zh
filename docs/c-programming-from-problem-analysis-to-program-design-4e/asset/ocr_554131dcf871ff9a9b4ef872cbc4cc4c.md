+   16. When determining which `else` matches which `if`, follow this rule: The `else` matches up with the closest previous `if` that does not already have an attached `else`.
+   17. Use a series of `else...if` for a long, nested, multiway statement.
+   18. The `switch` statement is considered a multiple selection structure that allows a large number of alternatives to be executed. The `switch` is used for equality comparisons only.
+   19. The `case` value with a `switch` statement must be a constant literal of the same type as the expression. It cannot be a variable.
+   20. With a `switch` statement, the occurrence of the first `case` value that matches the expression causes that case’s statement(s) to be executed. If no match is made with any of the `case` values, the statements associated with `default` are executed.
+   21. Having a `default` is not required, but it is a good idea always to include one.
+   22. There is no way to program a `switch` statement in C# to fall through to the code for the next `case`. After code is associated with a `case`, there must be a `break`. If used, the `default` statements must also end with a `break`.
+   23. Multiple cases in a `switch` statement can be associated with the same statements. This works like having a logical OR operator between each of the cases.
+   24. The `switch` statement cannot be used to test for a range of values, or to perform a relational test.
+   25. Also called the conditional operator, the ternary operator `? :` provides a shorthand way to express a simple `if...else` selection statement.
+   26. When an expression contains multiple operators, the precedence of the operators controls the order in which the individual operators are evaluated.
+   27. Equality operators have a lower precedence than relational operators; `&&` has a higher precedence than `||`, but both `&&` and `||` have lower precedence than the relational or equality operators. The very lowest precedence is the assignment operators.

# EXERCISES

+   1. The result of the expression `if (aValue == 10)` is:
+      a. true or false
+      b. 10
+      c. an integer value
+      d. aValue
+      e. determined by an input statement