This snippet prints:

Click here to view code image

```
Decimal:    1 2 000003 0 0 +4 -1
Hexadecimal: 5 a A 0x6
Octal:      12 012 04
Binary:     1010 0 b1010 0 b100
```

The first two numbers were just printed without giving any format information. The same output is generated when we ask for a decimal number with the format specifier "{:d}". The third number will be printed (minimally) 6 characters wide with leading 0s. The specifier + allows us to force printing the sign for all numbers. printf allows for specifying unsigned output of numbers. That leads to incorrect large numbers when the value to print is negative. The <format> library refrains from user declarations of unsigned output since this information is already contained in the type of the according argument. If somebody feels the urge to print a negative value as a large positive one, they must convert it explicitly.

The second line demonstrates that we can print values hexadecimally—both with lower-and uppercase for the digits larger than 9. The specifier "#" generates the prefix "0x" used in hexadecimal literals. Likewise, we can print the values as octals and binaries, optionally with the according literal prefix.

With floating-point numbers we have more formatting options:

Click here to view code image

```
print("Default:\t{} {:g} {:g}\n", 1.5, 1.5, 1e20);
print("Rounding:\t{:f} {:.0f} {:.22f}\n", 1.5, 1.5, 1.3);
print("Padding:\t{:05.2F} {:.2f} {:1.2 f}\n", 1.5, 1.5, 1.5);
print("Scientific:\t{:E} {:e}\n", 1.5, 1.5);
print("Hexadecimal:\t{:a} {:A}\n\n", 1.5, 1.3);
```

Then we get:

Click here to view code image

```
Default:    1.5 1.5 1e+20
Rounding:   1.500000 2 1.3000000000000000000000444089
Padding:    01.50 1.50 1.50
Scientific: 1.500000E+00 1.500000e+00
Hexadecimal: 0x1.8p+0 0X1.4 CCCCCCCCCCCDP+0
```