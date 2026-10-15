| From | To |
|---|---|
| byte | short, int, long, float, or double |
| short | int, long, float, or double |
| char | int, long, float, or double |
| int | long, float, or double |
| long | float or double |
| float | double |

# FIGURE 2.5 Java widening conversions

> KEY CONCEPT
> Narrowing conversions should be avoided because they can lose information.

Although widening conversions do not lose any information about the magnitude of a value, the widening conversions that result in a floating point value can lose precision. When converting from an int or a long to a float, or from a long to a double, some of the least significant digits may be lost. In this case, the resulting floating point value will be a rounded version of the integer value, following the rounding techniques defined in the IEEE 754 floating point standard.

Narrowing conversions are more likely to lose information than widening conversions are. They often go from one type to a type that uses less space to store a value, and therefore some of the information may be compromised. Narrowing conversions can lose both numeric magnitude and precision. Therefore, in general, they should be avoided. Figure 2.6 lists the Java narrowing conversions.

An exception to the space-shrinking situation in narrowing conversions is when we convert a byte (8 bits) or short (16 bits) to a char (16 bits). These are still

| From | To |
|---|---|
| byte | char |
| short | byte or char |
| char | byte or short |
| int | byte, short, or char |
| long | byte, short, char, or int |
| float | byte, short, char, int, or long |
| double | byte, short, char, int, long, or float |

# FIGURE 2.6 Java narrowing conversions