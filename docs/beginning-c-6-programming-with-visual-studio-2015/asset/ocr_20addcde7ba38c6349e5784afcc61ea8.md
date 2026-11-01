Here, the value stored in sourceVar is placed in destinationVar. When you output the variables with the two WriteLine() commands, you get the following output:

```
sourceVar val: a
destinationVar val: 97
```

Even though the two variables store the same information, they are interpreted in different ways using their type.

There are many implicit conversions of simple types; bool and string have no implicit conversions, but the numeric types have a few. For reference, Table 5-1 shows the numeric conversions that the compiler can perform implicitly (remember that chars are stored as numbers, so char counts as a numeric type).

# TABLE 5-1: Implicit Numeric Conversions

| TYPE | CAN SAFELY BE CONVERTED TO |
| byte | short, ushort, int, uint, long, ulong, float, double, decimal |
| sbyte | short, int, long, float, double, decimal |
| short | int, long, float, double, decimal |
| ushort | int, uint, long, ulong, float, double, decimal |
| int | long, float, double, decimal |
| uint | long, ulong, float, double, decimal |
| long | float, double, decimal |
| ulong | float, double, decimal |
| float | double |
| char | ushort, int, uint, long, ulong, float, double, decimal |

Don't worry — you don't need to learn this table by heart, because it's actually quite easy to work out which conversions the compiler can do implicitly. Back in Chapter 3, Tables 3-1, 3-2 and 3-3 showed the range of possible values for every simple numeric type. The implicit conversion rule for these types is this: Any type A whose range of possible values completely fits inside the range of possible values of type B can be implicitly converted into that type.

The reasoning for this is simple. If you try to fit a value into a variable, but that value is outside the range of values the variable can take, then there will be a problem. For example, a short type variable is capable of storing values up to 32767, and the maximum value allowed into a byte is 255, so there could be problems if you try to convert a short value into a byte value. If the short holds a value between 256 and 32767, then it simply won't fit into a byte.