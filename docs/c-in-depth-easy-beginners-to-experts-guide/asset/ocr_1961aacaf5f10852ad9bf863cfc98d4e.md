numerical data item. This flag is overridden by the + flag if both are present.

( # ) **(with o- and x- type conversion):-** causes octal and hexadecimal data items to be preceded by o and ox, respectively.

# **(with e-, f- and g- type conversion):-** causes a decimal point to be present in all a floating point numbers, even if the data item is a whole number.

# **Optional format specifiers:**

+   1. The field width specifier tells printf( ) how many columns on the screen should be used while printing a value. **For e.g.**

```
int a=5;
printf("%10d",a);
```

would give integer a a field width of 10 columns. Since the value cannot occupy the complete 10 columns, it will be right aligned leaving blank spaces on the left side.

**Thus output will be:**

5

+   2. if a minus sign is given with the format specifiers:

```
int a=5;
printf("%-10d",a);
```

would mean that the output should be left aligned leaving space at the right.
Show that output resulting from each of the following printf statements if the declaration is:
**float a=2.5, b=0.00005, c=3000;**

+   (i)

```
printf("%f %f %f", a, b, c);
output: 2.500000 0.000050 3000.000000
```

Note that each float number uses six places after decimal point.

+   (ii)

```
printf("%8f %8f %8f", a, b, c);
output: 2.500000e+00 5.000000e-05 3.000000e+03
```

+   (iii)

```
printf("%e %e %e", a, b, c);
output: 2.5000e+00  5.0000e-05  3.000e+03
```