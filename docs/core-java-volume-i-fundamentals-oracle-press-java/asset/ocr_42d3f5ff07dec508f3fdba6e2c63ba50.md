other operations, call `Byte.toUnsignedInt(b)` to get an int value between 0 and 255, then process the integer value and cast back to byte. The Integer and Long classes have methods for unsigned division and remainder.

# 3.3.2 Floating-Point Types

The floating-point types denote numbers with fractional parts. The two floating-point types are shown in **Table 3.2**.

# Table 3.2 Floating-Point Types

| Type | Storage Requirement | Range |
|---|---|---|
| `float` | 4 bytes | Approximately ±3.40282347×10^38 (6–7 significant decimal digits) |
| `double` | 8 bytes | Approximately ±1.79769313486231570×10^308 (15 significant decimal digits) |

The name `double` refers to the fact that these numbers have twice the precision of the `float` type. (Some people call these *double-precision* numbers.) The limited precision of `float` (6–7 significant digits) is simply not sufficient for many situations. Use `float` values only when you work with a library that requires them, or when you need to store a very large number of them.

Numbers of type `float` have a suffix F or f (for example, `3.14F`). Floating-point numbers without an F suffix (such as `3.14`) are always considered to be of type `double`. You can optionally supply the D or d suffix (for example, `3.14D`).

An e or E denotes a decimal exponent. For example, `1.729E3` is the same as `1729`.

> > **NOTE:**