# # Operators and Expressions



A value can be stored in a variable with the use of assignment operator. This assignment operator " = " is used in assignment expressions and assignment statements.

The operand on the left hand side should be a variable, while the operand on the right hand side can be any variable, constant or expression. The value of right hand operand is assigned to the left hand operand. Here are some examples of assignment expressions-

```
x = 8 /* 8 is assigned to x */
y = 5 /* 5 is assigned to y */
s = x+y-2 /* Value of expression x+y-2 is assigned to s */
y = x /* Value of x is assigned to y */
x = y /* Value of y is assigned to x */
```

The value that is being assigned is considered as value of the assignment expression. For example - 8 is an assignment expression whose value is 8.

We can have multiple assignment expressions also, for example-

x = y = z = 20

Here all the three variables x, y, z will be assigned value 20, and the value of the whole expression will be 20.

If we put a semicolon after the assignment expression then it becomes an assignment statement. For example these are assignment statements-

x = 8;
y = 5;
s = x+y-2;
x = y = z = 20;

When the variable on the left hand side of assignment operator also occurs on right hand side then we can avoid writing the variable twice by using compound assignment operators. For example-

x = x + 5

can also be written as-

x += 5

Here += is a compound assignment operator.

Similarly we have other compound assignment operators.

+   - x -=5 is equivalent to x = x - 5
+   - y *=5 is equivalent to y = y*5
+   - sum /=5 is equivalent to sum = sum / 5
+   - k%=5 is equivalent to k = k % 5



C has two useful operators increment ( ++ ) and decrement ( -- ). These are unary operators because they operate on a single operand. The increment operator ( ++ ) increments the value of the variable by 1 and decrement operator ( -- ) decrements the value of the variable by 1.