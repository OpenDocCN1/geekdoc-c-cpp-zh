# Math

The next few functions we'll cover are from the predefined method Math. These function can be extremely useful when calculations are required. Our first function is Math.Sqrt( ), which stands for the square root of a number. This function returns the square root of any value placed within its parentheses (see Example 2.28).

A second function linked to Math is the Math.Pow( ), which stands for an exponential power of a number (remember we can always substitute variables for literal constants). This could be used to reverse the square root, or with other powers such as cubes.

Our third and fourth functions are Math.Ceiling and Math.Floor, which are used to round real numbers to their highest or lowest whole value, respectively. The most important point to remember when working with these functions is that Ceiling always rounds up and Floor always rounds down, regardless of the size of the decimal value they're reading. That is, Math.Ceiling would round 3.2 to 4 and Math.Floor would round 3.9 to 3.0. Therefore, you'll have to decide which way you want to go before using either one.

# Trigonometric Functions [where x is a double/floating point value read in radians]:

![](bbox=[0.18, 0.6, 0.38, 0.75])

|  |  |
|---|---|
| sin θ = y/r | csc θ = r/y |
| cos θ = x/r | sec θ = r/x |
| tan θ = y/x | cot θ = x/y |

csc θ = 1/sin , sec θ = 1/cos , cot , = 1/tan , tan = sin θ /cos θ cot θ = cos θ/sin θ sin²θ+cos²θ θ = s/r (where s is the signed arc length)

# Example 2.28. A few common math functions.

```
```csharp
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            string input;
            double number1, number2, number3 = 2.0;
```
```