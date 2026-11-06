
The other formatting in the output statements indicates that variable `amount` is printed as a fixed-point value with a decimal point (specified in line 10 with the stream manipulator `fixed`) right justified in a field of 20 character positions (specified in line 27 with `setw(20)`) and two digits of precision to the right of the decimal point (specified in line 10 with manipulator `setprecision(2)`). We applied the stream manipulators `fixed` and `setprecision` to the output stream `cout` before the `for` loop because these format settings remain in effect until they’re changed—such settings are called **sticky settings** and they do *not* need to be applied during each iteration of the loop. However, the field width specified with `setw` applies *only* to the *next* value output. We discuss C++’s powerful input/output formatting capabilities in **Chapter 13**, Stream Input/Output: A Deeper Look.

## Performing the Interest Calculations with Standard Library Function `pow`

The `for` statement (lines 22–28) executes its body 10 times, varying the `unsigned int` control variable `year` from 1 to 10 in increments of 1. This loop terminates when `year` becomes 11. Variable `year` represents *n* in the problem statement.

C++ does *not* include an exponentiation operator, so we use the **standard library function** `pow` (line 24) from the header `<cmath>`. The call `pow(x, y)` calculates the value of *x* raised to the *y*th power. The function receives two `double` arguments and returns a `double` value.

Line 24 performs the calculation $a = p(1 + r)^n$, where $a$ is `amount`, $p$ is `principal`, $r$ is `rate` and $n$ is `year`.

The body of the `for` statement contains the calculation `1.0 + rate` as `pow`’s first argument. This calculation produces the same result each time through the loop, so repeating it in every iteration of the loop is wasteful.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_581_0.png)

**Performance Tip 5.1**

> *In loops, avoid calculations for which the result never changes—such calculations should typically be placed before the loop. Many of today’s sophisticated optimizing compilers will place such calculations before loops in the compiled code.*

### Floating-Point Number Precision and Memory Requirements

Variables of type `float` represent **single-precision floating-point numbers** and have approximately seven significant digits on most of today’s systems. Variables of type `double` represent **double-precision floating-point numbers**. These require twice as much memory as `float` variables and provide approximately 15 significant digits on most of today’s systems—approximately double the precision of `float` variables. Most programmers represent floating-point numbers with type `double`.

In fact, C++ treats all floating-point numbers you type in a program’s source code (such as 7.33 and 0.0975) as `double` values by default. Such values in the source code are known as **floating-point literals**. See **Appendix C** for the fundamental types’ value ranges.

### Floating-Point Numbers Are Approximations

In conventional arithmetic, floating-point numbers often arise as a result of division—when we divide 10 by 3, the result is 3.33333333…, with the sequence of 3s repeating infinitely. The computer allocates only a *fixed* amount of space to hold such a value, so clearly the stored floating-point value can be only an *approximation*. As you can see, `double` suffers from what we call **representational error**.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_582_0.png)

**Common Programming Error 5.6**

> *Using floating-point numbers in a manner that assumes they’re represented exactly (e.g., using them in comparisons for equality) can lead to incorrect results. Floating-point numbers are represented only approximately.*

Floating-point numbers have numerous applications, especially for measured values. For example, when we speak of a “normal” body temperature of 98.6 degrees Fahrenheit, we do not need to be precise to a large number of digits. When we read the temperature on a thermometer as 98.6, it may actually be 98.5999473210643. Calling this number simply 98.6 is fine for most applications involving body temperatures. Due to the imprecise nature of floating-point numbers, type `double` is preferred over type `float`, because `double` variables can represent floating-point numbers more precisely. For this reason, we use type `double` throughout the book.

### A Warning about Displaying Rounded Values

We declared variables `amount`, `principal` and `rate` to be of type `double` in this example. We’re dealing with fractional parts of dollars and thus need a type that allows decimal points in its values. Unfortunately, floating-point numbers can cause trouble. Here’s a simple explanation of what can go wrong when using `double` (or `float`) to represent dollar amounts (assuming that dollar amounts are displayed with two digits to the right of the decimal point): Two calculated `double` dollar amounts stored in the machine could be 14.234 (which would normally be rounded to 14.23 for display purposes) and 18.673 (which would normally be rounded to 18.67 for display purposes). When these amounts are added, they produce the internal sum 32.907, which would be rounded to 32.91 for display purposes. Thus, your output could appear as

```text
  14.23
+ 18.67
-------
  32.91
```

but a person adding the individual numbers as displayed would expect the sum to be 32.90. You’ve been warned!

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_584_0.png)

**Error-Prevention Tip 5.6**

> *Do not use variables of type* `double` *(or* `float`*) to perform precise monetary calculations. The imprecision of floating-point numbers can lead to errors.*

### Even Common Dollar Amounts Can Have Representational Error in Floating Point

Even simple dollar amounts, such as those you might see on a grocery or restaurant bill, can have representational errors when they’re stored as `double`s. To see this, we created a simple program with the declaration

```cpp
double d = 123.02;
```

then displayed variable `d`’s value with many digits of precision to the right of the decimal point—we ask you to do this in **Exercise 5.36**. The resulting output showed 123.02 as 123.0199999…, which is another example of a representational error. Though some dollar amounts can be represented precisely as `double`, many cannot. In the next section, we’ll build a class that represents and processes dollar amounts using only integer arithmetic. This eliminates the representational errors associated with `double` values, because integers are represented exactly.

## 5.7 Case Study: Integer-Based Monetary Calculations with Class `DollarAmount`

In **Chapter 3**, we developed an `Account` class. A typical dollar `Account` balance—such as $437.19—has a whole number of dollars (e.g., 437) to the left of the decimal point and a whole number of cents (e.g., 19) to the right. For simplicity, class `Account` represented its `balance` with type `int`, which of course limited balances to whole dollar amounts.

### Representing Dollar Amounts as Floating-Point Numbers

Rather than `int`, we need a type that allows us to represent a dollar amount as a number with a decimal point. In **Fig. 5.6**’s compound-interest example, we processed dollar amounts as type `double`. This introduced representational error and rounding issues:

1. There were representational errors, because we stored precise decimal dollar amounts and interest rates as `double`s. As you’ll see in this section, you can avoid these by performing all calculations using integer arithmetic—even interest calculations.

2. There was rounding of the floating-point values. We cannot avoid rounding on interest calculations, because they result in fractional pennies when working with dollar amounts. Those fractional pennies must be rounded to the hundredths place. With integer arithmetic we can exercise precise control over rounding without suffering the representational errors associated with floating-point calculations.

In addition, there are many points in monetary calculations in which rounding may occur. For example, on a restaurant bill, the tax could be calculated on each individual item, resulting in many separate rounding operations, or it could be calculated only once on the total bill amount—these alternate approaches could yield different results.

Performing monetary calculations with `double`s can cause problems for organizations that require precise dollar amounts—such as banks, insurance companies and businesses in general. A bank, for example, must keep precise track of all its customers’ balances. Imagine the problems that a large financial institution with millions of accounts would have if its customer balances didn’t “add up,” preventing the organization from tying out its books. For this reason, it’s crucial to perform monetary calculations using integer arithmetic rather than floating-point arithmetic. As you’ll see in our next example, even interest calculations can be done with integer arithmetic.
