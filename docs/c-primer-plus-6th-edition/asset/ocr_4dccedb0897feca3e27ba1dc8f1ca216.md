# Logical Expressions

The main() program uses a while loop to reject invalid input until the user gets it right. You could make the program friendlier by displaying the int limits when the input is out of range. After the input has been validated, the program assigns it to an int variable.

# Logical Operator Facts

As mentioned earlier in this chapter, the C++ logical OR and logical AND operators have a lower precedence than relational operators. This means that an expression such as this

+   x > 5 && x < 10

is interpreted this way:

```
(x > 5) && (x < 10)
```

The operator, on the other hand, has a higher precedence than any of the relational or arithmetic operators. Therefore, to negate an expression, you should enclose the expression in parentheses, like this:

```
!x > 5      // is it false that x is greater than 5
!x > 5      // is x greater than 5
```

Incidentally, the second expression is always false because !x can only have the values true or false, which converted to 1 or 0.

Logical AND operator has a higher precedence than the logical OR operator. Thus for this expression:

```
age > 30 && age < 45 || weight > 300
```

means the:

```
(age > 30 && age < 45) || weight > 300
```

That is, one condition is that age is in the range 31–44, and the second condition is that weight is greater than 300. The entire expression is true if one or the other or both of these conditions are true.

You can, use parentheses to tell the program the interpretation you want. For example, suppose you use && to combine the condition that age is greater than 50 or weight is greater than 300 with the condition that donation is greater than 1,000. You have to include the OR part within parentheses:

```
(age > 50 || weight > 300) && donation > 1000
```

Otherwise, the compiler combines the weight condition with the donation condition instead of the age condition.

Although the C++ operator precedence rules make it possible to write compound comparisons without using parentheses, the simplest course of action is to use parentheses to group the tests, whether or not the parentheses are needed. It makes the code easier to read, it doesn't force someone to look up some of the less commonly