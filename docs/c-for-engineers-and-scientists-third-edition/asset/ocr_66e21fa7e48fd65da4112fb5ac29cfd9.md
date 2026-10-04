# Chapter 1 11

Preliminary Two: Exponential and Scientific Notations

In exponential notation, the letter e stands for exponent. The following the e represents powers of 10 and indicates the number of places the decimal point should be moved to obtain the standard decimal value. The decimal point is moved to the right if the number is positive, or to the left if the after e is negative. the e3 in 1.62e3 moves the decimal point three places to the right, so the number becomes 1625.
The e-3 in 7.3e-3 means the decimal point three places to the left, so 7.3e-3 becomes .00731. Using these representations, Avogadro's number is 6.0221407e23 and 6.02214e19 in exponential and scientific notation, and the universal gravitational constant is written as 6.6742e-11 in exponential notation and 6.6742× 10⁻¹¹ in scientific notation.

As noted, exponential notation is used to enter very large or small numbers in a C++ program and will be used in Section 2.6, where very large numbers are required for the option.

# Using Scientific Notation

An essential part of engineering and scientific programming is understanding what formulas are to be used and verifying calculations, typically by hand. For evaluating formulas that use very large or small numbers, which isn't uncommon in the applications you'll be programming, scientific notation is convenient. The reason is that scientific notation permits using the following two basic rules, as they apply to

+   Rule 1: 10ⁿ × 10ᵐ for any values, positive or negative, of n and m
Examples: 10² × 10⁵ = 10⁷ (that is, 100 × 100,000 = 10,000,000)
10² × 10⁻⁵ = 10⁻³ (that is, 100 × .00001 = .01)
10² × 10⁻⁶ = 10⁻⁴ (that is, 100 × .000001 = .001)
10² × 10⁻⁷ = 10⁻⁵ (that is, 100 × .0000001 = .00001)
10² × 10⁻⁸ = 1

+   Rule 2: 10ⁿ / 10ᵐ for any positive or negative value of n

+   Examples: 10⁷ / 10² = 10⁵ (that is, .01)
10⁷ / 10¹⁰ = 10⁻³ (that is, .001)
10⁴ / 10¹ = 10³ (that is, 1000)
10⁴ / 10⁸ = 10⁻⁴ (that is, .00000)

Note that in scientific notation (as in exponential notation), it represents the actual number of zeros that follow the 1, but if the exponent is negative, it represents one less than the number of zeros after the decimal point and before the 1.

After you understand the basic rules of using scientific notation, you can combine them easily, as shown in this computation:

```
10² × 10⁸ = 10¹⁰n10⁴ / 10⁷ = 10⁻³
```