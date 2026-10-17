# Multiple-Alternative Decision Structure

# Nested Decision Control Structures

```
if (Boolean Expr 1) {
    block of statements 1
}
elseif (Boolean Expr 2) {
    block of statements 2
}
elseif (Boolean Expr 3) {
    block of statements 3
}
.
.
.
elseif (Boolean Expr N) {
    block of statements N
}
else {
    block of statements N+1
}
```

```
if (Boolean Expr 1) {
    block of statements 1
}
else {
    if (Boolean Expr 2) {
        block of statements 2
    }
    else {
        if (Boolean Expr 3) {
            block of statements 3
        }
        .
        .
        .
        else {
            if (Boolean Expr N) {
                block of statements N
            }
            else {
                block of statements N+1
            }
        }
    }
}
```

> Notice: The opposite conversion (from nested decision control structures to a multiple-alternative decision structure) is possible as long as the else keyword and the succeeding if statement (in the nested decision control structures) are side by side without any statements existing between them.

# Exercise 21.9-1 Converting the PHP Script

Rewrite the PHP script using nested decision control structures.

```
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));
echo "Enter a second number: ";
$y = trim(fgets(STDIN));
```