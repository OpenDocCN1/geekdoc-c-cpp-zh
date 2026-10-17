# 29.7  Converting from a Counted Loop Structure to a Pre-Test Loop Structure

The conversion from a counted loop structure to a pre-test loop structure is quite easy. All you need to do is get the `counter` variable of the `for` statement and use it within the `while` statement, as follows.

# Counted Loop Structure

```
for (counter = initial_value; counter OP1 final_value; counter = counter OP2 offset) {
    A statement or block of statements
}
```

![](bbox=[0.451, 0.364, 0.554, 0.421])

# Pre-Test Loop Structure

```
counter = initial_value;
while (counter OP1 final_value) {
    A statement or block of statements
    counter = counter OP2 offset;
}
```

where

+   - `counter` must always be a variable.
+   - `initial_value`, `final_value`, and `offset` can be a constant value or even a variable or an expression.
+   - `OP1` must be `<=` when counter increments and `>=` when counter decrements.
+   - `OP2` must be `+` when counter increments and `−` when counter decrements.

> **Remember!** Be careful not to forget to include the statement that increments or decrements the `counter` variable at the end of the pre-test loop structure, because otherwise the loop will iterate endlessly!

# Exercise 29.7-1    Converting the PHP Script

Rewrite the following PHP script using the pre-test loop structure.

```
<?php
    $x = 2;

    for ($i = -4; $i <= 4; $i = $i + 1) {
```