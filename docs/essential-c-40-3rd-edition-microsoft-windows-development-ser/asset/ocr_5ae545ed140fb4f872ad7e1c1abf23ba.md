often still a good practice to use parentheses to make the code more readable. This expression, for example:

```
fahrenheit = (celsius * 9.0 / 5.0) + 32.0;
```

is easier to interpret confidently at a glance than this one is:

```
fahrenheit = celsius * 9.0 / 5.0 + 32.0;
```

Developers should use parentheses to make code more readable, disambiguating expressions explicitly instead of relying on operator precedence.

# Assignment Operators (+=, -=, *=, /=, %=)

Chapter 1 discussed the simple assignment operator, which places the value of the right-hand side of the operator into the variable on the left-hand side. Other assignment operators combine common binary operator calculations with the assignment operator. Take Listing 3.10, for example.

# LISTING 3.10: Common Increment Calculation

```
int x;
x = x + 2;
```

In this assignment, first you calculate the value of x + 2 and then you assign the calculated value back to x. Since this type of operation is relatively frequent, an assignment operator exists to handle both the calculation and the assignment with one operator. The += operator increments the variable on the left-hand side of the operator with the value on the right-hand side of the operator, as shown in Listing 3.11.

# LISTING 3.11: Using the += Operator

```
int x;
x += 2;
```

This code, therefore, is equivalent to Listing 3.10.

Numerous other combination assignment operators exist to provide similar functionality. You can use the assignment operator in conjunction with not only addition, but also subtraction, multiplication, division, and the remainder operators, as Listing 3.12 demonstrates.