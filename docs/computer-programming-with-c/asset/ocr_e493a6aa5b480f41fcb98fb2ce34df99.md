> > The value of a will be printed for first occurrence of `%d`, b will be printed for second occurrence of `%d`, and the value of a+b will be printed for third occurrence of `%d` as shown in Figure 2.22.

Remember `%d` is a format specifier if we want to print integer types. In reality, there are different format specifiers for different types of data values to be printed. Table 2.2 gives the list of format specifiers supported by C/C++ to allow the programmer to print different types of values using `printf()`.

> **NOTES**
> 
> The format specifier `%s` is used to print string values. We have discussed strings in Chapter 6, where we will also learn about the usage of `%s`.

# 2.6.3 Format specifiers specific to floating point numbers

C/C++ supports additional format specifiers (for `float` and `double` types) which correctly choose either decimal or scientific way of the output format whichever is smaller to represent on screen.

| Format specifier | Description | Example | Output |
|---|---|---|---|
| `%g` | `%g` prints the value of float variable in the form of `%f` or `%e` whichever is smaller to represent on screen | `float v = 32000.9;`<br>`printf("Value is %g",v);`<br>`/*prints in decimal format (32000.9) because it is smaller to represent when compared to exponential format(3.20009e+004)*/` | **Value is**<br>`32000.9` |
| `%G` | `%G` prints the value of float variable in the form of `%f` or `%E` whichever is smaller to represent on screen | `float v=32000.9;`<br>`printf("Value is %G",v);`<br>`/*prints in decimal format (32000.9) because it is smaller to represent when compared to exponential format(3.20009E+004)*/` | **Value is**<br>`32000.9` |
| `%lg` | `%lg` prints the double variable in the form of `%lf` or `%le` whichever is smaller to represent on screen | `double v=32000120000.9;`<br>`printf("Value is %lg",v);`<br>`/*prints in exponential format (3.20001e+010) because it is smaller to represent when compared to decimal format(32000120000.9)*/` | **Value is**<br>`3.20001e+010` |