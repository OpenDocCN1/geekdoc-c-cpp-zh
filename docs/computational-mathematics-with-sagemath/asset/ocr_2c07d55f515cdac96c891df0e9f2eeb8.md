```
    sage: ( 1 + 2 * (3 + 5) ) * 2
    34
```

The \* character above stands for multiplication, which should not be omitted, even in expressions like 2*x*. The power operation is written ^ or \*\*:

```
    sage: 2^3
    8
    sage: 2**3
    8
```

and the division is denoted by /:

```
    sage: 20/6
    10/3
```

Please note the exact computation: the result of the above division, after simplification, is the rational number 10/3 and not an approximation like 3.33333. There is no limit¹ to the size of integers or rational numbers:

```
    sage: 2^10
    1024
    sage: 2^100
    1267650600228229401496703205376
    sage: 2^1000
    10715086071862673209484250490600018105614048117055336074437503883703510511249361224931983788156958581275946729175531468251871452856923140435984577574698574803934567774824230985421074605062371141877954182153046474983581941267398767559165543946077062914571196477686542167660429831652624386837205668069376
```

To obtain a numerical approximation, one simply writes one of the numbers with a decimal point (one could replace 20.0 by 20. or 20.000):

```
    sage: 20.0 / 14
    1.42857142857143
```

Besides, the numerical_approx function gives a numerical approximation of an expression:

```
    sage: numerical_approx(20/14)
    1.42857142857143
    sage: numerical_approx(2^1000)
    1.071508607186267e301
```

Numerical approximations can be computed to arbitrarily large precisions. For example, let us increase the precision to 60 digits to exhibit the periodicity of the digit expansion of a rational number:

¹ Except that due to the available memory of the computer used.