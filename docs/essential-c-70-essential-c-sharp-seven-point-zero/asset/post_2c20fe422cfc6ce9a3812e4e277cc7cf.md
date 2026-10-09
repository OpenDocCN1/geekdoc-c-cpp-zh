
## Output 4.4

9

You can use this trait of character types to determine how far two characters are from each other. For example, the letter f is three characters away from the letter c. You can determine this value by subtracting the letter c from the letter f, as Listing 4.6 demonstrates.

## Listing 4.6: Determining the Character Difference between Two Characters

```
int distance = 'f' - 'c';
System.Console.WriteLine(distance);
```

Output 4.5 shows the result of Listing 4.6.

## Output 4.5

3

### Special Floating-Point Characteristics

The binary floating-point types, float and double, have some special characteristics, such as the way they handle precision. This section looks at some specific examples, as well as some unique floating-point type characteristics.

A float, with seven decimal digits of precision, can hold the value 1,234,567 and the value 0.1234567. However, if you add these two floats together, the result will be rounded to 1234567, because the exact result requires more precision than the seven significant digits that a float can hold. The error introduced by rounding off to seven digits can become large compared to the value computed, especially with repeated calculations. (See also the Advanced Topic titled “Unexpected Inequality with Floating-Point Types” later in this section.)

Internally, the binary floating-point types actually store a binary fraction, not a decimal fraction. Consequently, “representation error” inaccuracies can occur with a simple assignment, such as `double number = 140.6f;`. The exact value of 140.6 is the fraction 703/5, but the denominator of that fraction is not a power of 2, so it cannot be represented exactly by a binary floating-point number. The value actually represented is the closest fraction with a power of 2 in the denominator that will fit into the 16 bits of a float.

Since the double can hold a more accurate value than the float can store, the C# compiler will actually evaluate this expression to `double number = 140.600006103516` because 140.600006103516 is the closest binary fraction to 140.6 as a float. This fraction is slightly larger than 140.6 when represented as a double.

### Guidelines

- AVOID binary floating-point types when exact decimal arithmetic is required; use the decimal floating-point type instead.

### Advanced Topic

#### Unexpected Inequality with Floating-Point Types

Because floating-point numbers can be unexpectedly rounded off to non-decimal fractions, comparing floating-point values for equality can be quite confusing. Consider Listing 4.7.

## Listing 4.7: Unexpected Inequality Due to Floating-Point Inaccuracies

```csharp
decimal decimalNumber = 4.2M;
double doubleNumber1 = 0.1F * 42F;
double doubleNumber2 = 0.1D * 42D;
float floatNumber = 0.1F * 42F;

Trace.Assert(decimalNumber != ((decimal)doubleNumber1));
// 1. Displays: 4.2 != 4.2000000625488
System.Console.WriteLine(
    $"{decimalNumber} != {(decimal)doubleNumber1}");

Trace.Assert(((double)decimalNumber != doubleNumber1));
// 2. Displays: 4.2 != 4.2000000625488
System.Console.WriteLine(
    $"{(double)decimalNumber} != {doubleNumber1}");

Trace.Assert((float)decimalNumber != floatNumber);
// 3. Displays: (float)4.2M != 4.2F
System.Console.WriteLine(
    $"(float){(float)decimalNumber}M != {floatNumber}F");

Trace.Assert(doubleNumber1 != ((double)floatNumber));
// 4. Displays: 4.2000000625488 != 4.2000002861029
System.Console.WriteLine(
    $"{doubleNumber1} != {(double)floatNumber}");

Trace.Assert(doubleNumber1 != doubleNumber2);
// 5. Displays: 4.20000006258488 != 4.2
System.Console.WriteLine(
    $"{doubleNumber1} != {doubleNumber2}");

Trace.Assert(floatNumber != doubleNumber2);
// 6. Displays: 4.2F != 4.2D
System.Console.WriteLine(
    $"{floatNumber}F != {doubleNumber2}D");

Trace.Assert((double)4.2F != 4.2D);
// 7. Displays: 4.19999980926514 != 4.2
System.Console.WriteLine(
    $"{(double)4.2F} != {4.2D}");

Trace.Assert(4.2F != 4.2D);
// 8. Displays: 4.2F != 4.2D
System.Console.WriteLine(
    $"{4.2F}F != {4.2D}D");
```

Output 4.6 shows the results of Listing 4.7.

## Output 4.6

```
4.2 != 4.20000006258488
4.2 != 4.20000006258488
(float)4.2M != 4.2F
4.20000006258488 != 4.20000028610229
4.20000006258488 != 4.2
4.2F != 4.2D
4.19999980926514 != 4.2
4.2F != 4.2D
```

The `Assert()` methods alert the developer whenever arguments evaluate to false. However, of all the `Assert()` calls in this code listing, only half have arguments that evaluate to true. In spite of the apparent equality of the values in the code listing, they are not actually equivalent due to the inaccuracies associated with float values.

### Guidelines

- AVOID using equality conditionals with binary floating-point types. Either subtract the two values and see if their difference is less than a tolerance, or use the decimal type.

You should be aware of some additional unique floating-point characteristics as well. For instance, you would expect that dividing an integer by zero would result in an error—and it does with data types such as int and decimal. The float and double types, however, allow for certain special values. Consider Listing 4.8, and its resultant output, Output 4.7.

## Listing 4.8: Dividing a Float by Zero, Displaying NaN

```csharp
float n = 0f;
// Displays: NaN
System.Console.WriteLine(n / 0);
```

## Output 4.7

```
NaN
```

In mathematics, certain mathematical operations are undefined, including dividing zero by itself. In C#, the result of dividing the float zero by zero results in a special **Not a Number** value; all attempts to print the output of such a number will result in NaN. Similarly, taking the square root of a negative number with `System.Math.Sqrt(-1)` will result in NaN.

A floating-point number could overflow its bounds as well. For example, the upper bound of the float type is approximately $3.4 \times 10^{38}$. Should the number overflow that bound, the result would be stored as **positive infinity**, and the output of printing the number would be Infinity. Similarly, the lower bound of a float type is $-3.4 \times 10^{38}$, and computing a value below that bound would result in **negative infinity**, which would be represented by the string -Infinity. Listing 4.9 produces negative and positive infinity, respectively, and Output 4.8 shows the results.

## Listing 4.9: Overflowing the Bounds of a float

```csharp
// Displays: -Infinity
System.Console.WriteLine(-1f / 0);
// Displays: Infinity
System.Console.WriteLine(3.402823e+38f * 2f);
```

## Output 4.8

```
-Infinity
Infinity
```

Further examination of the floating-point number reveals that it can contain a value very close to zero without actually containing zero. If the value exceeds the lower threshold for the *float* or *double* type, the value of the number can be represented as **negative zero** or **positive zero**, depending on whether the number is negative or positive, and is represented in output as -0 or 0.

### Compound Mathematical Assignment Operators (+=, -=, *=, /=, %=)

Chapter 1 discussed the simple assignment operator, which places the value of the right-hand side of the operator into the variable on the left-hand side. **Compound mathematical assignment operators** combine common binary operator calculations with the assignment operator. For example, consider Listing 4.10.

## Listing 4.10: Common Increment Calculation

```csharp
int x = 123;
x = x + 2;
```

In this assignment, first you calculate the value of x + 2, and then you assign the calculated value back to x. Since this type of operation is performed relatively frequently, an assignment operator exists to handle both the calculation and the assignment with one operator. The += operator increments the variable on the left-hand side of the operator with the value on the right-hand side of the operator, as shown in Listing 4.11.

## Listing 4.11: Using the += Operator

```csharp
int x = 123;
x += 2;
```

This code, therefore, is equivalent to Listing 4.10.

Numerous other compound assignment operators exist to provide similar functionality. You can also use the assignment operator with subtraction, multiplication, division, and remainder operators (as demonstrated in Listing 4.12).

## Listing 4.12: Other Assignment Operator Examples

```csharp
x -= 2;
x /= 2;
x *= 2;
x %= 2;
```
