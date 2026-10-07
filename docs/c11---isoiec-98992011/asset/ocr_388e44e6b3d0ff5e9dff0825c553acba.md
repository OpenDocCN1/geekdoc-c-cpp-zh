# 7.20.1.1 Exact-width integer types

+   1 The typedef name intN_t designates a signed integer type with width N, no padding bits, and a two's complement representation. Thus, int8_t denotes a signed integer type with a width of 8 bits.

+   2 The typedef name uintN_t designates an unsigned integer type with width N and no padding bits. Thus, uint24_t denotes such an unsigned integer type with a width of 24 bits.

+   3 These types are optional. However, if an implementation provides integer types with widths of 8, 16, 32, or 64 bits, no padding bits, and (for the signed types) that have a two's complement representation, it shall define the corresponding typedef names.

# 7.20.1.2 Minimum-width integer types

+   1 The typedef name int_leastN_t designates a signed integer type with width of at least N, such that no signed integer type with lesser size has at the specified width. Thus, int_least32_t denotes a signed integer type with a width of at least 32 bits.

+   2 The typedef name uint_leastN_t designates an unsigned integer type with width of at least N, such that no unsigned integer type with lesser size has at the specified width. Thus, uint_least16_t denotes an unsigned integer type with a width of at least 16 bits.

+   3 The following types are required:

```
int_least8_t          uint_least8_t
int_least16_t        uint_least16_t
int_least32_t        uint_least32_t
int_least64_t        uint_least64_t
```

All other types of this form are optional.

# 7.20.1.3 Fastest-width integer types

+   1 Each of the following types designates an integer type that is usually fastest(262) to operate with all integer types that have at least the specified width.

+   2 The type int_fastN_t designates the fastest signed integer type with a width of at least N. The typedef name uint_fastN_t designates the fastest unsigned integer type with a width of at least N.