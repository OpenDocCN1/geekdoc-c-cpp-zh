# 4.8. MORE ARITHMETIC OPERATORS

```
x op= exp;
```

where

+   * x is a variable.
* op= an arithmetic operator combined with the assignment operator; for our purposes, the most useful to use are +=, -=, *=, /= and %=.
* exp is an expression compatible with the variable x.

Arithmetic reassignment statements of this form are equivalent to

```
x = x op exp;
```

This means the statement

```
x *= y + z;
```

is equivalent to

```
x = x * (y + z);
```

The version using the arithmetic reassignment does not require parentheses. The arithmetic assignment is especially handy if a variable with a long name is to be modified; consider

```
temporary_filename_length = temporary_filename_length / (y + z);
```

versus

```
Do not accidentally reverse the order of the symbols for the arithmetic assignment operators, like in the statement
x += 5;
Notice that the + and = symbols have been reversed. The compiler interprets statement as if it had been written
x = +5;
that is, assignment and the unary operator. This assigns x to exactly five instead of increasing it by five.
Similarly.
x -= 3;
would assign -3 to x instead of decreasing x by three.
```

Appendix E examines some additional arithmetic operators available in C++.