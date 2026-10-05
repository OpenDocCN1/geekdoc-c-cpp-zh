On the one hand, the return value of theString is conveniently included in the message here, and on the other hand, it would have an effect if you had defined operator== for the two arguments.

If you do not want to use ==, instead use BOOST_level_BITWISE_EQUAL(exp, res), where the arguments are compared directly in memory.

Instead of equality using ...EQUAL, you can also use GE, GT, LE, LT, and NE for >=, >, <=, and != respectively.

You must exercise special caution when you want to compare floating-point numbers. A test for equality using == is out of the question. Instead, check if exp and res are close enough by providing a third parameter that specifies "close enough" means:

```
double sqSumDif(double a, double b) {
    return a*a+b*b-a*b;
}
BOOST_CHECK_CLOSE(sqSumDif(4.1, 3.9), 16.03, 0.01);
```

The output here is

```
info: difference% between sqSumDif(4.1, 3.9)(16.029999999999998) and \
16.03(16.030000000000001) doesn't exceed 0.01%
```

because the actual imprecise result deviates from the expected one, but it is within the specified tolerance of 0.01%. Here, you should specify an appropriate tolerance on a case-by-case basis. The 0.01% tolerance is probably quite coarse for such a simple calculation,