call a static method by specifying the class name followed by the member-access operator (.) and the method name, as in

```
ClassName.MethodName(arguments)
```

C# does not include an exponentiation operator, C# will not use Math's static method to perform the compound-interest calculation. The expression

```
Math.Pow(x, y)
```

calculates the value of x raised to the yth power. The method receives two double arguments and returns a double. Lines 19–20 in Fig. 6 perform the calculation

```
a = p (1 + r)^n
```

from the problem statement, where a is the amount, p is the principal, r is the rate and n is the year. In this calculation, we need to multiply the decimal value principal by a double value (the value returned by the call to Math.Pow) may not implicitly convert double to a decimal type, or vice versa, because of the possible loss of information in either conversion, so line 20 contains a (decimal) cast that explicitly converts Math.Pow's return value to a decimal.

The statement's body contains the calculation 1.0 + rate, which appears as an argument to the Math.Pow. In fact, this calculation produces the same result each time through the loop, repeating the calculation in every iteration of the loop is wasteful.

# Performance Tip 6.2

In loops, avoid calculations for which the result never changes—calculations should typically be placed before the loop. Optimizing compilers will typically do this for you.

![](bbox=[0.143, 0.507, 0.857, 0.587])

# 6.6.2 Formatting with Field Widths and Alignment

After each calculation, line 23

```
Console.WriteLine("${year,4}{amount,20:C}");
```

displays the year and the amount on deposit at the end of the year. The interpolation expression

```
{year,4}
```

formats the year. The integer 4 after the comma indicates that the value output should be displayed with a field width of 4—that is,WriteLine displays the value with at least four character positions (one or two characters in this example), the value is right-aligned if the output is fewer than four characters wide (by default—padded by two or three spaces, depending on the year. If the value to be output were more than four character positions wide, the field width would be extended to the right to accommodate the entire value—this would push the column to the right, upsetting the neat columns of our tabular output. Similarly, the interpolation expression

```
{amount,20:C}
```