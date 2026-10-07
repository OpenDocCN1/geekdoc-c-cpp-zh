# Type Conversions

casts i to type float. In other words, the program makes an internal copy of the value of i in floating-point format.

When would you use a typecast as an arithmetic expression? The most common use is to avoid losing the fractional part of the answer in an integer division. Listing 21.1 illustrates this. You should compile and run this program.

# Input ▼

LISTING 21.1 casting.c: When One Integer Is Divided by Another, Any Fractional Part of the Answer Is Lost

```
1: #include <stdio.h>
2:
3: int main( void )
4: {
5:     int i1 = 100, i2 = 40;
6:     float f1;
7:
8:     f1 = i1/i2;
9:     printf("%f\n", f1);
10: return(0);
11: }
```

# Output ▼

2.000000

# Analysis ▼

The answer displayed by the program is 2.000000, but 100/40 evaluates to 2.5. What happened? The expression i1/i2 on line 8 contains two type int variables. Following the rules established earlier today, you should determine the value of the expression i1/i2 is type int itself. This is because the two operands are both of type int. As such, the result can represent only the fractional part of the answer is lost.

You might think assigning the result of i1/i2 to a float variable promotes it to type float. This is correct, but it's too late; the fractional part of the answer is already gone.

To avoid this sort of inaccuracy, you must cast the int variables to type float. If one of the variables is cast to type float, the previous rules tell you that the other variable is promoted automatically to type float, and the value of the expression is also type float. The fractional part of the answer is thus preserved. To demonstrate this, change line 8 in the source code so that the assignment statement reads as follows:

![](bbox=[0.913, 0.816, 0.953, 0.846])