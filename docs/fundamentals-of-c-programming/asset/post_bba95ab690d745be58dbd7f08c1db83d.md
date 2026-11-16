
Figure 4.6 The cyclic nature of 32-bit unsigned integers. Adding 1 to 4,294,967,295 produces 0, one position clockwise from 4,294,967,295. Subtracting 4 from 2 yields 4,294,967,294, four places counter-clockwise from 2.

![](img/e84ad11adb18201d71595b31ce6c9eff_73_0.png)

```
4294967293 + 1 = 4294967294
4294967293 + 2 = 4294967295
4294967293 + 3 = 0
```

In fact, Visual C++'s 32-bit unsigneds follow the cyclic pattern shown in Figure 4.6.

In the figure, an addition moves a value clockwise around the circle, while a subtraction moves a value counterclockwise around the circle. When the numeric limit is reached, the value rolls over like an automobile odometer. Signed integers exhibit a similar cyclic pattern as shown in Figure 4.7.

In the case of signed integers, as Figure 4.7 shows, adding one to the largest representable value produces the smallest negative value. Listing 4.14 (integeroverflow.cpp) demonstrates.

### Listing 4.14: integeroverflow.cpp

```
#include <iostream>

int main() {
    int x = 2147483645; // Almost the largest possible int value
    std::cout << x << " + 1 = " << x + 1 << '\n';
    std::cout << x << " + 2 = " << x + 2 << '\n';
    std::cout << x << " + 3 = " << x + 3 << '\n';
}
```

Figure 4.7 The cyclic nature of 32-bit signed integers. Adding 1 to 2,147,483,647 produces -2,147,483,648, one position clockwise from 2,147,483,647. Subtracting 5 from -2,147,483,645 yields 2,147,483,646, five places counterclockwise from -2,147,483,645.

![](img/e84ad11adb18201d71595b31ce6c9eff_74_0.png)

Listing 4.14 (integeroverflow.cpp) prints

```
2147483645 + 1 = 2147483646
2147483645 + 2 = 2147483647
2147483645 + 3 = -2147483648
```

Attempting to exceed the maximum limit of a numeric type results in overflow, and attempting to exceed the minimum limit is called underflow. Integer arithmetic that overflow or underflow produces a valid, yet incorrect integer result. The compiler does not check that a computation will result in exceeding the limit of a type because it is impossible to do so in general (consider adding two integer variables whose values are determined at run time). Also importantly, an overflow or underflow situation does not generate a run-time error. It is, therefore, a logic error if a program performs an integral computation that, either as a final result or an intermediate value, is outside the range of the integer type being used.

## 4.8.2 Floating-point Implementation

The standard C++ floating point types consist of float, double, and long double. Floating point numbers can have fractional parts (decimal places), and the term floating point refers to the fact the decimal point in a number can float left or right as necessary as the result of a calculation (for example, 2.5 x 3.3 = 8.25, two one-decimal place values produce a two-decimal place result). As with the integer types, the different floating-point types may be distinguished by the number of bits of storage required and corresponding range of values. The type float stands for single-precision floating-point, and double stands for double-precision floating-point. Floating point numbers serve as rough approximations of mathematical real numbers, but as we shall see, they have some severe limitations compared to actual real numbers.

On most modern computer systems floating-point numbers are stored internally in exponential form according to the standard adopted by the Institute for Electrical and Electronic Engineers (IEEE 754). In the decimal system, scientific notation is the most familiar form of exponential notation:

One mole contains 6.023 × 10^23 molecules.

Here 6.023 is called the mantissa, and 23 is the exponent.

The IEEE 754 standard uses binary exponential notation; that is, the mantissa and exponent are binary numbers. Single-precision floating-point numbers (type float) occupy 32 bits, distributed as follows:

| Mantissa | 24 bits |
| Exponent | 7 bits |
| Sign | 1 bit |
| Total | 32 bits |

Double-precision floating-point numbers (type double) require 64 bits:

| Mantissa | 52 bits |
| Exponent | 11 bits |
| Sign | 1 bit |
| Total | 64 bits |

Figure 4.8 A tiny float simplified binary exponential value

![](img/e84ad11adb18201d71595b31ce6c9eff_76_0.png)

The details of the IEEE 754 implementation are beyond the scope of this book, but a simplified example serves to highlight the limitations of floating-point types in general. Recall the fractional place values in the decimal system. The place values, from left to right, are

| ... | 10,000 | 1,000 | 100 | 10 | 1 | . | 1/10 | 1/100 | 1/1000 | 1/10000 | ... |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ... | 10^4 | 10^3 | 10^2 | 10^1 | 10^0 | . | 10^-1 | 10^-2 | 10^-3 | 10^-4 | ... |

Each place value is one-tenth the place value to its left. Move to the right, divide by ten; move to the left, multiply by ten. In the binary system, the factor is two instead of ten:

| ... | 16 | 8 | 4 | 2 | 1 | . | 1/2 | 1/4 | 1/8 | 1/16 | ... |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ... | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 | . | 2^-1 | 2^-2 | 2^-3 | 2^-4 | ... |

As in our unsigned tiny example (see Section 4.8.1), consider a binary exponential number that consists of only five bits—far fewer bits than either floats or doubles in C++. We will call our mythical floating-point type tiny float. The first three bits of our 5-bit tiny float type will represent the mantissa, and the remaining two bits store the exponent. The three bits of the mantissa all appear to the right of the binary point. The base of the 2-bit exponent is, of course, two. Figure 4.8 illustrates such a value.

To simplify matters even more, neither the mantissa nor the exponent can be negative. Thus, with three bits, the mantissa may assume one of eight possible values. Since two bits constitute the exponent of tiny floats, the exponent may assume one of four possible values. Table 4.4 lists all the possible values that tiny float mantissas and exponents may assume. The number shown in Figure 4.8 is thus

```
(1 x 2^-1 + 0 x 2^-2 + 1 x 2^-3) x 2^(1x2^1 + 0x2^0) = (1/2 + 1/8) x 2^2
= 5/8 x 4
= 2.5
```

Table 4.5 combines the mantissas and exponents to reveal all possible tiny float values that we can represent with the 32 different bit strings made up of five bits. The results are interesting.

The range of our tiny float numbers is 0...7. Just stating the range is misleading, however, since it might give the impression that we may represent any value between 0 and 7 down to the 1/8th place. This, in fact, is not true. We can represent 2.5 with this scheme, but we have no way of expressing 2.25. Figure 4.9 plots all the possible tiny float values on the real number line.

| Bit String | Binary Value | Decimal Value |
| :--- | :--- | :--- |
| 000 | 0.000₂ | 0/2 + 0/4 + 0/8 = 0.000 |
| 001 | 0.001₂ | 0/2 + 0/4 + 1/8 = 0.125 |
| 010 | 0.010₂ | 0/2 + 1/4 + 0/8 = 0.250 |
| 011 | 0.011₂ | 0/2 + 1/4 + 1/8 = 0.375 |
| 100 | 0.100₂ | 1/2 + 0/4 + 0/8 = 0.500 |
| 101 | 0.101₂ | 1/2 + 0/4 + 1/8 = 0.625 |
| 110 | 0.110₂ | 1/2 + 1/4 + 0/8 = 0.750 |
| 111 | 0.111₂ | 1/2 + 1/4 + 1/8 = 0.875 |

| Bit String | Binary Value | Decimal Value |
| :--- | :--- | :--- |
| 00 | 2⁰⁰₀₂ | 2⁰ = 1 |
| 01 | 2⁰⁰₁₂ | 2¹ = 2 |
| 10 | 2⁰¹₀₂ | 2² = 4 |
| 11 | 2⁰¹₁₂ | 2³ = 8 |

Table 4.4: The eight possible mantissas and four possible exponents that make up all tiny float values

Figure 4.9 A plot of all the possible tiny float numbers on the real number line. Note that the numbers are more dense near zero and become more sparse moving to the right. The precision in the range 0...1 is one-eighth. The precision in the range 1...2 is only one-fourth, and over the range 2...4 it drops to one-half. In the range 4...7 our tiny float type can represent only whole numbers.

![](img/e84ad11adb18201d71595b31ce6c9eff_77_0.png)

Table 4.5 and Figure 4.9 reveal several troubling issues about our tiny float type:

- 1. There are many gaps; for example, the value 2.4 is missing and thus cannot be represented exactly (2.5 is the closest approximation). As another example, 0.75 and 1.75 both appear, but 2.75 is missing.

- 2. The scheme duplicates some numbers; for example, three different bit patterns represent the decimal value 0.5:

  0.100 x 2⁰⁰ = 0.010 x 2⁰¹ = 0.001 x 2¹⁰ = 0.5₁₀

  This duplication limits the number of different values that can be represented by a given number of bits. In our tiny float example 12 of the 32 bit strings (37.5%) are redundant.

- 3. The numbers are not uniformly dense. There are more values nearer to zero, and the numbers become more sparse farther away from zero.

Our unsigned tiny type discussed in Section 4.8.1 exhibits none of these weaknesses. All integers in a given range (0...31) are present, no two bit strings represent the same value, and the integers are uniformly distributed across their specified range. While the standard integer types provided by C++ have much greater ranges than our unsigned tiny type, they all share these same qualities: all values in their ranges are present, and all bit strings represent unique integer values. The standard floating-point types provided by C++ use many more bits than our tiny float type, yet they exhibit the same problems shown to a much smaller degree: missing values, multiple bit patterns representing the same values, and
