the maximum field width of input data. If the length of input is more than this maximum field width then the values are not stored correctly. For example-

```
scanf ("%2d%3d", &a, &b );
```

(i) When input data length is less than the given field width, then the input values are unaltered and stored in given variables.

Input-
6 39

Result-
6 is stored in a and 39 is stored in b.

(ii) When input data length is equal to the given field width, then the input values are unaltered and stored in given variables.

Input-
26 394

Result-
26 is stored in a and 394 is stored in b.

(iii) When input data length is more than the given field width, then the input values are altered and stored in the variable as -

Input-
269 3845

Result-
26 is stored in a and 9 is stored in b and the rest of input is ignored.

# 3.4.2 Format For Integer Output

%wd

Here w is the integer number specifying the minimum field width of the output data. If the length of the variable is less than the specified field width, then the variable is right justified with leading blanks. For example -

```
printf("a=%3d, b=%4d", a, b );
```

(i) When the length of variable is less than the width specifier.

Value of variables-
78 9

![](bbox=[0.45, 0.75, 0.85, 0.82])

The width specifier of first data is 3 while there are only 2 digits in it, so there is one leading blank. The width specifier of second data is 4 while there is only 1 digit, so there are 3 leading blanks.

(ii) When the length of the variable is equal to the width specifier

Value of variables-
263 1941