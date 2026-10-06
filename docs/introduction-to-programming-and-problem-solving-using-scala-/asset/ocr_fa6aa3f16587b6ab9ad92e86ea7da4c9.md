# Introduction to Programming and Problem-Solving Using Scala

| Type | e Bits | m bits | bias | Min | Max |
|---|---|---|---|---||}{
| Float | 8 | 23 | 127 | -3.408235E38 | 3.408235E38 |
| Double | 11 | 52 | 1023 | -1.79769313462317E308 | 1.79769313462317E308 |

TABLE 2.2: Floating point types with sizes and ranges.

not Real numbers in the sense you are used to with arbitrary precision. Floating point numbers have limited precision. Unlike the integers, they can be overflowed. Unlike integers, they are fundamentally imprecise because they represent fractional values with a finite number of bits. The real implications of these are seen in the following example.

```
scala>1.0-9-0.1
res39: Double = -2.775557561526814E-17
```

To understand why this happens, consider the simple fraction, 1/3, the decimal representation of 0.3333... In order to write this fraction accurately in decimal, you need an infinite number of digits. In math we can denote this by putting in three dots or putting a line over the digits that are repeated. For floating point values, the digits simply cut off when you get to the end of the mantissa. As such, they are not exact and the circuitry in the computer employs a rounding scheme to deal with this. This imprecise is invisible most of the time, but one immediate implication of it is that you cannot trust two floating point numbers to be equal if they were calculated using arithmetic. It means that you should not use floating point numbers for programs that involve money. The decimal value 0.1 is a repeating fraction in binary, hence the problem in the example above, and as such, is not perfectly represented. Instead you should use an integer type and store cents instead of dollars.

# 2.6 The math Object

While on the topic of numbers, there are quite a few standard functions that you might want to do with numbers beyond addition, subtraction, multiplication, and division. There are a few other things you can get from operators that we will discuss later. Things like square root, logarithms, and trigonometric functions are not operators. They are found as methods in the math object. You can use tab completion in the REPL to see all the different methods that you can call on math and values stored in it.

```
scala> math.
ScalaNumericConversions max
BigDecimal             min
BigInt                 abs
E                      acos    package
Equiv                  asin    pow
Fractional             atan    random
IEEEFloat              atan2    rint
Integral               cbrt    round
LowPriorityEquiv       ceil    signum
LowPriorityOrderingImplits cos sin
Numeric                cosh    sinh
Ordered                exp     sqrt
Ordering               expml   tan
```