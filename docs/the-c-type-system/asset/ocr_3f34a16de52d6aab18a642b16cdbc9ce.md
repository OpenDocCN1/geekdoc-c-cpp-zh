number may be relatively larger or smaller than the original value. The difference between two neighboring exact representations is proportional to the magnitude of those numbers, so the rounding difference of a very large number will generally be much greater than that for a very small number. Calculations with multiple numbers that have been rounded will compound the resulting rounding error, a problem that isn’t restricted to either very large or very small numbers. Listing 5-2 compares two double values that we might intuitively expect to be equal.

```
double x = 0.3;
double y = 0.1 + 0.2;

Assert.That(x == y, Is.True);
```

Listing 5-2: A simple floating-point calculation

This test fails because none of the constant values can be represented exactly in the format of a double. The values given to x and y will be rounded to the nearest representable value. On top of that, the result of the addition has an inexact representation and so is rounded again, producing a value that differs from the value assigned to x. The test for equality between x and y fails because the values differ in their least significant digits.

Subtracting one floating-point number from another can also produce unexpected results: if the two numbers are nearly equal, the result will have values only in those least significant places, which is exactly where rounding will be noticeable. The consequence is that some or all of the significant digits in the result may be lost, a problem sometimes called cancellation.

Rounding and cancellation issues are inherent in the IEEE-754 representation of floating-point values and not specific to C#. It’s possible to alleviate some of the problems that arise from them, however, depending on exactly what we want to achieve.

# Mitigating the Limitations of Rounding and Cancellation

The magnitude of rounding is predictable, as it’s directly related to the precision of the binary representation. Precision here means the number of binary digits that can be stored in the type. Importantly, that means any number without an exact representation in a given type will always round the same way for the same type.

The compounded error caused by repeated calculations is harder to predict, and the order of operations in a calculation can significantly affect the result. Performing the same sequence of operations twice might even produce different results, depending on factors such as optimization and the location of the result being stored. A complete analysis of the different approaches to comparing floating-point numbers is far too large a topic to cover here, but in essence, rather than comparing floating-point numbers for exact equality, we can provide an implementation that determines whether two numbers are approximately equal.