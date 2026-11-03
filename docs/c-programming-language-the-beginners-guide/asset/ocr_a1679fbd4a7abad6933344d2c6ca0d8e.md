# Logical Operators

The C language’s logical operators are used to compare two or more expressions. The operators determine whether the result is true or false. Three operators are available to use:

+   - `&&` logical AND
+     - `||` logical OR
+     - `!` logical NOT

These are often written in all caps, so that they are not confused with the regular words. For an AND operation to be true, both conditions must be AND. For an OR operator, either of the conditions must be OR. And for the NOT operator, the condition must be false, which is backwards, but that’s how NOT works—NOT.

As an example, the AND operator evaluates two conditions below:

```
a = 7;
if( a > 0 && a < 10 )
TRUE && TRUE == TRUE
```