
### 3.5.2 Mathematical Functions and Constants

The Math class contains an assortment of mathematical functions that you may occasionally need, depending on the kind of programming that you do.

To take the square root of a number, use the sqrt method:

```
double x = 4;
double y = Math.sqrt(x);
System.out.println(y); // prints 2.0
```

> **NOTE:** There is a subtle difference between the `println` method and the `sqrt` method. The `println` method operates on the `System.out` object. But the `sqrt` method in the `Math` class does not operate on any object. Such a method is called a *static* method. You can learn more about static methods in Chapter 4.

The Java programming language has no operator for raising a quantity to a power. You must use the pow method in the Math class. The statement

```
double y = Math.pow(x, a);
```

sets y to be x raised to the power a (x^a). The pow method’s parameters are both of type double, and it returns a double as well.

The floorMod method aims to solve a long-standing problem with integer remainders. Consider the expression n % 2. Everyone knows that this is 0 if n is even and 1 if n is odd. Except, of course, when n is odd and negative. Then it is -1. Why? When the first computers were built, someone had to make rules for how integer division and remainder should work for negative operands. Mathematicians had known the optimal (or “Euclidean”) rule for a few hundred years: always leave the remainder ≥ 0. But, rather than open a math textbook, those pioneers came up with rules that seemed reasonable but are actually inconvenient.

Consider this problem. You compute the position of the hour hand of a clock. An adjustment is applied, and you want to normalize it to a number between 0 and 11. That is easy: (position + adjustment) % 12. But what if the adjustment is negative? Then you might get a negative number. So you have to introduce a branch, or use ((position + adjustment) % 12 + 12) % 12. Either way, it is a hassle.

The floorMod method makes it easier: floorMod(position + adjustment, 12) always yields a value between 0 and 11. (Unfortunately, floorMod gives negative results for negative divisors, but that situation doesn’t often occur in practice.)

The Math class supplies the usual trigonometric functions:

```
Math.sin
Math.cos
Math.tan
Math.atan
Math.atan2
```

and the exponential function with its inverse, the natural logarithm, as well as the decimal logarithm:

```
Math.exp
Math.log
Math.log10
```

Finally, two constants denote the closest possible approximations to the mathematical constants π and *e*:

```
Math.PI
Math.E
```

> **TIP:** You can avoid the Math prefix for the mathematical methods and constants by adding the following line to the top of your source file:
> 
> ```java
> import static java.lang.Math.*;
> ```
> 
> For example:
> 
> ```java
> System.out.println("The square root of \u03C0 is " + sqrt(PI));
> ```
> 
> We discuss static imports in Chapter 4.

> **NOTE:** The methods in the Math class use the routines in the computer’s floating-point unit for fastest performance. If completely predictable results are more important than performance, use the StrictMath class instead. It implements the algorithms from the “Freely Distributable Math Library” (www.netlib.org/fdlibm), guaranteeing identical results on all platforms.

> **NOTE:** The Math class provides several methods to make integer arithmetic safer. The mathematical operators quietly return wrong results when a computation overflows. For example, one billion times three (1000000000 * 3) evaluates to -1294967296 because the largest int value is just over two billion. If you call `Math.multiplyExact(1000000000, 3)` instead, an exception is generated. You can catch that exception or let the program terminate rather than quietly continue with a wrong result. There are also methods `addExact`, `subtractExact`, `incrementExact`, `decrementExact`, `negateExact`, all with int and long parameters.

### 3.5.3 Conversions between Numeric Types

It is often necessary to convert from one numeric type to another. Figure 3.1 shows the legal conversions.

![](img/127bccebb2cfadea3f02579edaad63c3_82_0.png)

Figure 3.1 Legal conversions between numeric types

The six solid arrows in Figure 3.1 denote conversions without information loss. The three dotted arrows denote conversions that may lose precision. For example, a large integer such as 123456789 has more digits than the float type can represent. When the integer is converted to a float, the resulting value has the correct magnitude but loses some precision.

```
int n = 123456789;
float f = n; // f is 1.23456792E8
```

When two values are combined with a binary operator (such as n + f where n is an integer and f is a floating-point value), both operands are converted to a common type before the operation is carried out.

- If either of the operands is of type `double`, the other one will be converted to a `double`.
- Otherwise, if either of the operands is of type `float`, the other one will be converted to a `float`.
- Otherwise, if either of the operands is of type `long`, the other one will be converted to a `long`.
- Otherwise, both operands will be converted to an `int`.

### 3.5.4 Casts

In the preceding section, you saw that int values are automatically converted to double values when necessary. On the other hand, there are obviously times when you want to consider a double as an integer. Numeric conversions are possible in Java, but of course information may be lost. Conversions in which loss of information is possible are done by means of casts. The syntax for casting is to give the target type in parentheses, followed by the variable name. For example:

```
double x = 9.997;
int nx = (int) x;
```

Now, the variable nx has the value 9 because casting a floating-point value to an integer discards the fractional part.

If you want to round a floating-point number to the nearest integer (which in most cases is a more useful operation), use the Math.round method:

```
double x = 9.997;
int nx = (int) Math.round(x);
```

Now the variable nx has the value 10. You still need to use the cast (int) when you call round. The reason is that the return value of the round method is a long, and a long can only be assigned to an int with an explicit cast because there is the possibility of information loss.

> **CAUTION:** If you try to cast a number of one type to another that is out of range for the target type, the result will be a truncated number that has a different value. For example, (byte) 300 is actually 44.

> **C++ NOTE:** You cannot cast between boolean values and any numeric type. This convention prevents common errors. In the rare case when you want to convert a boolean value to a number, you can use a conditional expression such as `b ? 1 : 0`.

### 3.5.5 Combining Assignment with Operators

There is a convenient shortcut for using binary operators in an assignment. For example,

```
x += 4;
```

is equivalent to

```
x = x + 4;
```

(In general, place the operator to the left of the = sign, such as *= or %=.)

> **NOTE:** If the operator yields a value whose type is different from that of the left-hand side, then it is coerced to fit. For example, if x is an int, then the statement
> 
> ```java
> x += 3.5;
> ```
> 
> is valid, setting x to (int)(x + 3.5).

### 3.5.6 Increment and Decrement Operators

Programmers, of course, know that one of the most common operations with a numeric variable is to add or subtract 1. Java, following in the footsteps of C and C++, has both increment and decrement operators: n++ adds 1 to the current value of the variable n, and n-- subtracts 1 from it. For example, the code

```
int n = 12;
n++;
```

changes n to 13. Since these operators change the value of a variable, they cannot be applied to numbers themselves. For example, 4++ is not a legal statement.

There are two forms of these operators; you’ve just seen the postfix form of the operator that is placed after the operand. There is also a prefix form, ++n. Both change the value of the variable by 1. The difference between the two appears only when they are used inside expressions. The prefix form does the addition first; the postfix form evaluates to the old value of the variable.

```
int m = 7;
int n = 7;
int a = 2 * m++; // now a is 16, m is 8
int b = 2 * ++n; // now b is 14, n is 8
```

We recommend against using ++ inside expressions because this often leads to confusing code and annoying bugs.
