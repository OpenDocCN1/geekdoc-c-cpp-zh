This prints

```
```
1234.57        (general)
1234.567890    (fixed)
1.234568e+003  (scientific)
```
```

The manipulators **fixed**, **scientific**, and **defaultfloat** are used to select floating-point formats; **defaultfloat** is the default format (also known as the *general format*). Now, we can write

```
```cpp
cout << 1234.56789 << '\t'
    << fixed << 1234.56789 << '\t'
    << scientific << 1234.56789 << '\n';
cout << 1234.56789 << '\n';            // floating format "sticks"
cout << defaultfloat << 1234.56789 << '\t'
                                        // the default format for
                                        // floating-point output
    << fixed << 1234.56789 << '\t'
    << scientific << 1234.56789 << '\n';
```
```

This prints

```
```
1234.57    1234.567890    1.234568e+003
1.234568e+003               // scientific manipulator "sticks"
1234.57    1234.567890    1.234568e+003
```
```

In summary, the basic floating-point output-formatting manipulators are:

| | |
| :--- | :--- |
| **Floating-point formats** | |
| **fixed** | use fixed-point notation |
| **scientific** | use mantissa and exponent notation; the mantissa is always in the [1:10) range; that is, there is a single nonzero digit before the decimal point |
| **defaultfloat** | choose **fixed** or **scientific** to give the numerically most accurate representation, within the precision of **defaultfloat** |

# ### 11.2.4 Precision

By default, a floating-point value is printed using six total digits using the **defaultfloat** format. The most appropriate format is chosen and the number is rounded to give the best approximation that can be printed using only six digits (the default precision for the **defaultfloat** format). For example:

```
```
1234.567 prints as 1234.57
1.2345678 prints as 1.23457
```
```