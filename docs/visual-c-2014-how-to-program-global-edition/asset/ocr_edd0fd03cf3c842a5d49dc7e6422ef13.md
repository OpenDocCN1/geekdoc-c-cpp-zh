# 7.6 Argument Promotion and Casting

double without changing its value. However, converting a double to an int truncates the fractional part of the double value—part of the value is lost. Double variables can hold much larger (and much smaller) than int variables, assigning a double to an int can cause a loss of information when the double value doesn't fit in the int. Converting large integers to small integer types (e.g., long to int) can also produce incorrect results.

# 7.6.1 Promotion Rules

The promotion rules apply to expressions containing values of two or more simple types and to simple-type values passed as arguments to methods. Each value is promoted to the appropriate type (Actually, the expression uses a temporary copy of each promoted value—the types of the original values remain unchanged.) Figure 7.4 shows the simple types affected and to which they can be promoted. Values of all simple types can also be implicitly converted to type object. We demonstrate implicit conversions in Chapter 19.

| Type | Conversion types |
|---|---|
| bool | no possible implicit conversions to other simple types |
| byte | ushort, short, int, uint, long, decimal, float or double |
| char | ushort, int, uint, long, decimal, float or double |
| decimal | no possible implicit conversions to other simple types |
| double | no possible implicit conversions to other simple types |
| float | double |
| int | long, decimal, float or double |
| long | decimal, float or double |
| sbyte | short, int, long, decimal, float or double |
| short | int, long, decimal, float or double |
| uint | long, long, decimal, float or double |
| long | decimal, float or double |
| ushort | int, uint, long, decimal, float or double |

> Fig. 7.4 | Explicit conversions between simple types.

# 7.6.2 Sometimes Explicit Casts Are Required

By default

To prevent a compilation error in cases where implicit conversion between simple types, the compiler requires you to use a cast operator to force the conversion. This enables you to "take control" from the compiler. This essen-