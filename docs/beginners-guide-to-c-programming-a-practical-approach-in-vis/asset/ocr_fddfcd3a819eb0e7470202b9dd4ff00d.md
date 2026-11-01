| From type | To type |
|---|---|
| byte | short, ushort, long, ulong, float, int, uint, double, decimal |
| sbyte | int, float, decimal, short, long, double |
| short | int, float, long, double, decimal |
| ushort | int, uint, long, ulong, double, float, decimal |
| int | float, double, long, decimal |
| uint | float, double, long, decimal, ulong |
| long | float, decimal, double |
| float | double |
| char | int, float, double, long, decimal, uint, ulong |

Table 7.4. Permitted implicit conversions

+   - **Explicit conversions:** Explicit conversions enable us to convert a data type to another type which has a smaller allocated space. Remember that this is not a permitted operation in implicit conversion as we stated above. We do explicit conversion by informing the compiler that an explicit conversion will take place as follows:

```
double myDouble = 1.25;
short newShort = (short) myDouble;
```

Code 7.26

In the first line, we declared the variable named myDouble and initialized it as 1.25. In the second line, we declare a short type variable called myShort. Remember that short type variables have 2 bytes of space while double types have 8 bytes of space therefore it is illegal to convert a double type to a short type implicitly. Because of this we informed the compiler that we'll convert the contents of the myDouble to a short type by the expression (short). In the end, we converted 1.25 to short and assigned it to the newShort variable. However, myShort will hold only 1 instead of 1.25 therefore we lose some information with explicit conversion.