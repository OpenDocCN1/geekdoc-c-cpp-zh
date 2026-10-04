10. (Conversion) Your company will soon open a new office in France. So that it can do business there, your manager has asked you to prepare a comprehensive package that performs the following American-to metric conversions on demand:

| Measure | American | Metric | Formula |
|---|---|---|--|
| distance | inch | centimeter | 2.54 cm/in |
| | foot | meter | 0.305 m/ft |
| | yard | meter | 0.9144 m/yd |
| | mile | kilometer | 1.6109 km/mi |
| temperature | Fahrenheit | Celsius | C = (5/9)(F - 32) |
| weight | pound | kilogram | 0.454 kg/lb |
| | ounce | gram | 28.35 gm/oz |
| currency | dollar | franc | entered by the user, about 5 francs/$ |
| capacity | quart | liter | 0.946 liter/qt |
| | teaspoon | milliliter | 4.9 ml/tsp |
| math | degree | radian | rad = (π/180)(degree) |
| | degree | grad | grad = (200/180)(degree)|

11. (Numerical) Heron's formula for the area, A, of a triangle with sides of length a, b, and c

```
A = \sqrt{[s(s-a)(s-b)(s-c)]
```

where

```
s = (a+b+c)/2
```

Write, test, and execute a function that accepts the values of a, b, and c as parameters from a calling function, and calculates the values of s and s[s-a)(s-b)(s-c). If this quantity is positive, the function calculates A. If the quantity is negative, a, b, and c do not form a triangle, and the function should return A = -1. The value of A should be returned by the function.

12. (Numerical) A formula to raise a real number, a, to the real power, b, is given by the formula

```
a^b = e^{b*ln(a)}
```

where a must be positive and b must be positive or 0. Using this formula, write a function named power () that accepts a and b as real values and returns a^b.

13. (Numerical) A fraction-handling program contains this menu:

+   - A. Add two fractions
- B. Convert a fraction to decimal
- C. Multiply two fractions
- Q. Quit

A Write C++ code for the program with stub functions for the choices.