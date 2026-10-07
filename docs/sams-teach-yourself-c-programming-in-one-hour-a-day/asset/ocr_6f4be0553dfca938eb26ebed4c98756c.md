The compound operators provide a convenient shorthand, the advantages of which are particularly evident when the variable on the left side of the assignment operator has a long name. With all other assignment statements, a compound assignment statement is an expression and evaluates to the value assigned to the left side. Thus, executing the following statements results in both x and z having the value 14:

```
x = 12;
z = x += 2;
```

# # The Conditional Operator

The conditional operator is C's ternary operator, meaning that it takes three operands. Its syntax is

```
exp1 ? exp2 : exp3;
```

If exp1 evaluates to true (that is nonzero), the entire expression evaluates to the value of exp2. If exp1 evaluates to false (that is zero), the entire expression evaluates as the value of exp3. For example, the following statement assigns the value i to x if y is true and assigns 100 to x if y is false:

```
x = y ? 1 : 100;
```

Likewise, to make z equal to the larger of x and y, you could code

```
z = (x > y) ? x : y;
```

Perhaps you've noticed that the conditional operator functions somewhat like an if statement. The preceding statement could also be written like this:

```
if (x > y)
  z = x;
else
  z = y;
```

The conditional operator can not be used in all situations in place of an if...else construction, but the conditional operator is more concise. The conditional operator can also be used in places you can't use an if statement, such as inside a call to another function such as a single statement:

```
printf("The larger value is %d", (x > y) ? x : y);
```

# # The Comma Operator

The comma is frequently used in C as a simple punctuation mark, serving to separate variable declarations, function arguments, and so on. In certain situations, the comma