# 2.2 Constants and Variables 79

The following example shows the declaration of float variables and constants.

```
float load;
float area;
float stress;
const float PI = 3.1415937; /* seven significant digits */
```

The three variable declarations can be combined into one statement as follows:

```
float load, area, stress;
```

Variables load, area, and stress are floating point variables that hold values limited to 7 decimal digits. There is an exact binary equivalent for 0.5 and 0.25 but not for 0.1. Therefore, float values may be more approximate than exact.

+   41.23 is stored as approximately .412300 × 10^2
.0000423 is stored as approximately .412300 × 10^-4
2.0/3.0 is stored as approximately .6666666 × 10^0
2.0 * 7.754321 is stored as approximately .150864 or .150864 × 10^2

Engineering and science applications deal with decimal numbers. In some engineering and science applications the number of digits is important for precision. The float variables hold only seven decimal digits, the last of which may be inexact. For higher precision the float data type is not sufficient.

Data Type double: When engineering and science applications require higher precision, data type double also must be used. Data type double is also required by some of the library functions. A variable declared with data type double will be allocated eight bytes of storage, which can hold up to fifteen decimal digits, the last of which may be inexact.

The declaration of double-precision variables is as follows:

```
double atomic_number, planets_distance;
```

Variables atomic_number and planets_distance are allocated eight bytes of storage. Most of the time high-precision values are represented in scientific notation. For example a number 123.456789 is represented in scientific notation as 1.23456789E02.

A named constant of data type double should be defined when it is declared.

```
const double PI = 3.1415926523472; /* thirteen significant digits */
```