The numbers line up to the right. That alignment works well for numbers, but not for strings. Usually, you want strings to line up at the left. You use the left and right manipulators to set the alignment. The following example uses left alignment for a string and then switches back to right alignment for a number:

```
out_file << left << setw(10) << word << right << setw(10) << number;
```

The default format for floating-point numbers is called *general* format. That format displays as many digits as are specified by the *precision* (6 by default), switching to scientific notation for large and small numbers. For example,

```
out_file << 12.3456789 << " " << 123456789.0;
```

yields

```
12.3457 1.23457e+08
```

The *fixed* format prints all values with the same number of digits after the decimal point. In the fixed format, the same numbers are displayed as

```
12.345679 123456789.000000
```

> Use the fixed and setprecision manipulators to format floating-point numbers with a fixed number of digits after the decimal point.

Use the fixed manipulator to select that format, and use the setprecision manipulator to change the precision. For example,

```
out_file << fixed << setprecision(2) << 1.2 << " " << 1.235
```

yields

```
1.20 1.24
```

**Table 2. Stream Manipulators**

| Manipulator | Purpose | Example | Output |
|---|---|---|---|
| `setw` | Sets the field width of the next item only. | `out_file << setw(6) << 123 << endl`<br>`<< 123 << endl`<br>`<< setw(6) << 12345678;` | `123`<br>`123`<br>`12345678` |
| `setfill` | Sets the fill character for padding a field. (The default character is a space.) | `out_file << setfill('0') << setw(6)`<br>`<< 123;` | `000123` |
| `left` | Selects left alignment. | `out_file << left << setw(6) << 123;` | `123` |
| `right` | Selects right alignment (default). | `out_file << right << setw(6) << 123;` | `123` |
| `fixed` | Selects fixed format for floating-point numbers. | `double x = 123.4567;`<br>`out_file << x << endl << fixed << x;` | `123.457`<br>`123.456700` |
| `setprecision` | Sets the number of significant digits for general format, the number of digits after the decimal point for fixed format. | `double x = 123.4567;`<br>`out_file << fixed << x << endl`<br>`<< setprecision(2) << x;` | `123.456700`<br>`123.46` |