```
C:\MyPrograms>gcc conv.c -o conv.exe
C:\MyPrograms>conv
String 12right converts to Integer: 12
String -65.8 converts to Integer: -65
String x13 converts to Integer: 0
Decimal 12 is Binary: 1100
Decimal 12 is Octal: 14 chars: 2
Decimal 12 is Hexadecimal: c chars: 1
C:\MyPrograms>_
```

![](bbox=[0.11, 0.26, 0.22, 0.34])

The itoa() function is very useful, but because it is not part of the ANSI standard it is not supported by all compilers – it is, however, supported by the GNU C Compiler featured in this book.

![](bbox=[0.11, 0.44, 0.22, 0.53])

Unlike the itoa() function, sprintf() cannot convert to binary because there is no format specifier for binary numbers.