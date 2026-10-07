# The if Statement

value of number is not less than zero,this program statement is automatically skipped. (If it is already positive, you don't want to negate it.) The absolute value of number is then displayed by the program, and program execution ends.

Let's look at another program that uses the if statement. We will add one more method to the Fraction class, called convertNum. This method will provide the value of a fraction as a real number. In other words, it will return the value by the denominator and return the result as a double precision value. So if you have the fraction 1/2, you want the method to return the value 0.5.

The declaration for such a method might look like this:

```
- (double) convertNum;
```

This is how you could write its definition:

```
- (double) convertNum;
{
    return numerator / denominator;
}
```

Well, not quite. As it's defined, this method actually has two serious problems. Can you spot them? The first is to arithmetic conversions. Recall that numerator and denominator are both integer instances. What happens when you divide two integers? Correct, it is done as an integer division! If you wanted to convert the fraction 1/2, the correct code would give you zero! This is easily corrected by using the type operator to convert one or both of the operands to a floating-point value before the division takes place:

```
(double) numerator / denominator
```

Recalling the relatively high precedence of this operator, the value of numerator is first converted to double before the division occurs. Furthermore, you don't need to convert the denominator because the rules of arithmetic conversion take care of you.

The second problem with this method is that you should check for division by zero. The invoker of this method could inadvertently forget to set the denominator of the fraction or have set the denominator of the fraction to zero, and you don't want your program to terminate abnormally.

The modified version of the convertNum method appears here:

```
- (double) convertNum
{
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}
```

We decided to return the special value NAN (which stands for Not A Number) if the denominator of the fraction is zero. This symbol is defined in a system header file called math.h, which gets automatically imported into your program.