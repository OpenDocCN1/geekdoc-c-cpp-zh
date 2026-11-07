# 13.5 **TYPE CONVERSION**

When we are working with fundamental data types, we sometimes use mixed types in an expression and expect the system to make them the same type according to the rules of conversion. For example, in the following expression statement, which finds the perimeter of a circle with radius 5, the system does two conversions from integer 5 to double 5.0 and integer 2 to 2.0 to find the perimeter:

```
```cpp
double perimeter = 2 * 5 * 3.1415;
```
```

We can do the same, with some limitation, to change a fundamental type to a user-defined type and vice versa.

# 13.5.1 Fundamental Type to Class Type

If we need to change a fundamental type to a class type (when it makes sense), we create a new parameter constructor (also referred to as conversion constructor). For example, we can convert an integer to a fraction and we can convert a real number to a fraction. In both cases, we create a constructor with one parameter.

# Converting an Integer to a Fraction

This can be done easily using a constructor that takes one integer parameter that is set as numerator; the denominator is set to 1.

# EXAMPLE 13.10

Table 13.16 shows how we can convert an integer to a Fraction object. We can add a fraction to an integer because the compiler changes the integer 4 to the fraction 4/1 before addition.

```
```cpp
Fraction fract1 (2, 5);
Fraction fract2 = fract1 + 4
```
```

# Converting a Real Number to a Fraction

We can use a constructor to convert a real number to a fraction. A fraction can be a real number. For example, the fraction 7/4 is the real number 1.75. This means that we can also convert a real number, such as 1.75, to its corresponding fraction representation. Given the value 1.75, we can rewrite it as 175/100 and then normalize it to get 7/4.

**Table 13.16 — Converting an integer value to a fraction**

```cpp
// Declaration
Fraction (int n);

// Definition
Fraction :: Fraction (int n)
: numer (n), denom (1)
{
}
```