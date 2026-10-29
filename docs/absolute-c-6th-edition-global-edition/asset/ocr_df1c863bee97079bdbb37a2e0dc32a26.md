# Overloading Unary Operators

In addition to the binary operators, such as + in x + y, C++ has unary operators, such as the operator - when it is used to mean negation. A unary operator is an operator that takes only one operand (one argument). In the following statement, the unary operator - is used to set the value of a variable x equal to the negative of the value of the variable y:

```
x = -y;
```

The increment and decrement operators, ++ and --, are other examples of unary operators.

You can overload unary operators as well as binary operators. For example, we have overloaded the minus operator - for the type Money (Display 8.1) so that it has both a unary and a binary operator version of the subtraction/negation operator -. For example, suppose your program contains this class definition and the following code:

```
Money amount1(10), amount2( ), amount3;
```

Then the following sets the value of amount3 to amount1 minus amount2:

```
amount3 = amount1 - amount2;
```

The following will, then, output $4.00 to the screen:

```
amount3.output( );
```

On the other hand, the following will set amount3 equal to the negative of amount1:

```
amount3 = -amount1;
amount3.output( );
```

You can overload the ++ and -- operators in ways similar to how we overloaded the negation operator in Display 8.1. If you overload the ++ and -- operators following the example of the minus sign - in Display 8.1, then the overloading definition will apply to the operator when it is used in prefix position, as in ++x and --x. Later in this chapter we will discuss overloading ++ and -- more fully and will then explain how to overload these operators for use in the postfix position.

# Overloading as Member Functions

In Display 8.1 we overloaded operators as stand-alone functions defined outside the class. It is also possible to overload an operator as a member operator (member function). This is illustrated in Display 8.2.

Note that when a binary operator is overloaded as a member operator, there is only one parameter, not two. The calling object serves as the first parameter. For example, consider the following code:

```
Money cost(1, 50), tax(0, 15), total;
 total = cost + tax;
```

When + is overloaded as a member operator, then in the expression cost + tax the variable cost is the calling object and tax is the single argument to +.