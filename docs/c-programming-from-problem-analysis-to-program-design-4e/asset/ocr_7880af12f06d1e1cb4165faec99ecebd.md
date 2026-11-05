# Floating-Point Types

If you need to keep the decimal portion, the value cannot be stored in an integral data type, such as an int. Floating-point values can be specified in scientific notation with an exponent or in standard decimal notation. Very large or small numbers can be specified. The general form of exponential syntax is:

```
n.ne±P
```

With the scientific notation syntax in the preceding example, n is the decimal number; P is the number of decimal positions to move left or right; and the + or – indicate the direction the decimal should be moved. A plus sign indicates that the decimal is moved P positions to the right to form the standard decimal equivalent value. The syntax rules in C# allow the e to be uppercase or lowercase. The ± in the notation indicates that a +, –, or neither can be added. If there is no + or –, + is assumed. Example 2–4 shows examples of converting from scientific to standard decimal notation.

# EXAMPLE 2.4

+   3.2e+5 is equivalent to 320000
+   1.76e-3 is equivalent to .00176
+   6.892e8 is equivalent to 689200000

Because the first value includes an "e+5", the decimal is moved to the right five positions. The second statement in the preceding examples moves the decimal position three positions to the left. The last statement moves the decimal to the right eight positions, which places five significant zeros onto the end of the value.

As Table 2-10 indicates, a value with up to 15 to 16 decimal places can be placed in a double. The floating-point types conform to IEEE 754 specifications. For more information, you can read about the IEEE standard at the Web site http://standards.ieee.org/. The following are examples of floating-point variable declarations.

TABLE 2-10 Values and sizes for floating-point types

| Type | Numeric range | Precision | Size |
|---|---|---|---|
| float | ±1.5 × 10^-45 to ±3.4 × 10^38 | 7 digits | 32-bit |
| double | ±5.0 × 10^-324 to ±1.7 × 10^308 | 15–16 digits | 64-bit |