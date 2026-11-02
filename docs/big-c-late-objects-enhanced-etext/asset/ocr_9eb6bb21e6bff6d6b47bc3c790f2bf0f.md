![](bbox=[0.13, 0.14, 0.2, 0.32])

# Common Error 3.2

# Confusing = and ==

The rule for the correct usage of = and == is very simple: In tests, always use == and never use =. If it is so simple, why can't the compiler be helpful and flag any errors? Actually, the C++ language allows the use of = inside tests. To understand this, we have to go back in time. The creators of C, the predecessor to C++, were very frugal. They did not want to have special values true and false. Instead, they allowed any numeric value inside a condition, with the convention that 0 denotes false and any non-0 value denotes true. Furthermore, in C and C++ assignments have values. For example, the value of the assignment expression floor = 13 is 13.

These two features—namely that numbers can be used as truth values and that assignments are expressions with values—conspire to make a horrible pitfall. The test

```
if (floor = 13) // ERROR
```

is legal C++, but it does not test whether floor and 13 are equal. Instead, the code sets floor to 13, and because that value is not zero, the condition of the if statement is always fulfilled.

Fortunately, most compilers issue a warning when they encounter such a statement. You should take such warnings seriously. (See Programming Tip 3.5 for more advice about compiler warnings.)

Some shell-shocked programmers are so nervous about using = that they use == even when they want to make an assignment:

```
floor == floor - 1; // ERROR
```

This statement tests whether floor equals floor - 1. It doesn't do anything with the outcome of the test, but that is not an error. Some compilers will warn that “the code has no effect”, but others will quietly accept the code.

![](bbox=[0.13, 0.64, 0.2, 0.82])

# Common Error 3.3

# Exact Comparison of Floating-Point Numbers

Floating-point numbers have only a limited precision, and calculations can introduce roundoff errors. You must take these inevitable roundoffs into account when comparing floating-point numbers. For example, the following code multiplies the square root of 2 by itself. Ideally, we expect to get the answer 2:

![](bbox=[0.75, 0.68, 0.95, 0.82])

© caracterdesign/iStockphoto.

Take limited precision into account when comparing floating-point numbers.

```
double r = sqrt(2.0);
if (r * r == 2)
{
    cout << "sqrt(2) squared is 2" << endl;
}
else
{
    cout << "sqrt(2) squared is not 2 but " << setprecision(18) << r * r << endl;
}
```

This program displays
sqrt(2) squared is not 2 but 2.0000000000000044

It does not make sense in most circumstances to compare floating-point numbers exactly. Instead, we should test whether they are close enough. That is, the magnitude of their