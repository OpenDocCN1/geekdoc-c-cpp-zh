side of the field width. (To force a number to be printed with a + sign, you will have to call `cout.setf(ios::showpos);` when you no longer want the + signs to print, you may call `cout.unsetf(ios::showpos)`.)

By the way, you can see that `setf` and `unsetf` are both member functions of the `cout` output stream. They are defined in `<iostream>` and may be used with any output stream. The arguments, such as `ios::left`, are also defined in the header file `<iostream>`.

# Format of Float and Double Numbers

The format for printing `float` and `double` numbers is also controlled by the `setf` functions. Here are three examples:

```
cout.setf(ios::fixed,
          ios::floatfield);
cout.setf(ios::scientific,
          ios::floatfield);
cout.setf(0, ios::floatfield);
```

Fixed-point notation. The first example, using `ios::fixed`, causes numbers to be printed in fixed-point notation, which is the common way of writing numbers with a decimal point. For example, the number 19% will be printed as 19.25.

Scientific notation. The second example, using `ios::scientific`, causes numbers to be printed in scientific notation, consisting of a number times some power of 10. For example, the large number 1.8 x 10^6 will be printed as 1.8e16. The letter e indicates the exponent.

Automatic notation. The third form, using the number 0 as the argument, causes C++ to select the format that it thinks is best for a number (either fixed-point or scientific notation).

If you don't specify one of the three formats, then C++ uses the automatic format. Once a format is set, it remains in place for all subsequent outputs.

# Precision of Float and Double Numbers

Output streams have a precision function with one integer argument to determine how many digits are printed for each number. For example, this statement sets the precision to 12:

```
cout.precision(12);
```

(An alternative is `cout << setprecision(12)`, which uses `setprecision` from `<iomanip>`.) With a precision of 12, the fixed-point and scientific notations will both have 12 digits of accuracy after the decimal point. The automatic notation will have a total of 12 significant digits. Once you set the precision, it stays in effect for all subsequent outputs.

When the automatic notation is used, trailing zeros and the decimal point are not always printed. For example, the `double` number 123.0 will be printed as 123 (with no decimal point). With a precision of 12, the number 19/4 will be printed with no trailing zeros, resulting in 19.25 (rather than 19.250000000000). You may force the decimal point and trailing zeros for fixed-point numbers with the function call `cout.setf(ios::showpoint)`. You may revert to the usual method of automatic