# else-if statement: Multiple Alternative Decision Statement

The pseudo-code example below:

```
if x is less than zero then
    set y equal to -1
else if x is equal to zero then
    set y equal to 0
else
    set y equal to 1
```

can be read as follows:

If the condition "x is less than zero" is true, set the value of y to -1.

Otherwise, the condition "x is less than zero" is a false. So if the condition "x is equal to zero" is true, set the value of y to 0.

Otherwise, the conditions "x is less than zero" and "x is equal to zero" are both false. So we set the value of y to 1.

The else if statement is used whenever an if statement has nesting only inside the else clause. The syntax looks like this:

```
if (expression1) {
    statement1;
} else if (expression2) {
    statement2;
} else if (expression3) {
    statement3;
} else {
    statement4;
}
```