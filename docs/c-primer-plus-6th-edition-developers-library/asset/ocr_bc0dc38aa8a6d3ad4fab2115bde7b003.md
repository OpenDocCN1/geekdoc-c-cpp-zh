# Fastest Minimum-Width Types

For a particular system, some integer representations can be faster than others. For example, int_least16_t might be implemented as short, but the system might do arithmetic faster using type int. So inttypes.h also defines the fastest type for representing at least a certain number of bits. These types always exist. In some cases, there might be no clear-cut choice for fastest; in that case, the system simply specifies one of the choices. Table RS.VI.3 lists fastest minimum-width types, format specifiers, and value limits.

Table RS.VI.3 Fastest Minimum-Width Types

| Type Name | printf() Specifier | scanf() Specifier | Minimum Value | Maximum Value |
|---|---|---|---|---|
| int_fast8_t | PRIFASTd8 | SCNFASTd8 | INT_FAST8_MIN | INT_FAST8_MAX |
| int_fast16_t | PRIFASTd16 | SCNFASTd16 | INT_FAST16_MIN | INT_FAST16_MAX |
| int_fast32_t | PRIFASTd32 | SCNFASTd32 | INT_FAST32_MIN | INT_FAST32_MAX |
| int_fast 64_t | PRIFASTd64 | SCNFASTd64 | INT_FAST64_MIN | INT_FAST64_MAX |
| uint_fast 8_t | PRIFASTu8 | SCNFASTu8 | 0 | UINT_FAST8_MAX |
| uint_fast 16_t | PRIFASTu16 | SCNFASTu16 | 0 | UINT_FAST16_MAX |
| uint_fast 32_t | PRIFASTu32 | SCNFASTu32 | 0 | UINT_FAST32_MAX |
| uint_fast 64_t | PRIFASTu64 | SCNFASTu64 | 0 | UINT_FAST64_MAX |

# Maximum-Width Types

Sometimes you may want the largest integer type available. Table RS.VI.4 lists these types. They may, in fact, be wider than long long or unsigned long long, because a system may provide additional types wider than the required types.

Table RS.VI.4 Maximum-Width Types

| Type Name | printf() Specifier | scanf() Specifier | Minimum Value | Maximum Value |
|---|---|---|---|---|
| intmax_t | PRIdMAX | SCNdMAX | INTMAX_MIN | INTMAX_MAX |
| uintmax_t | PRIuMAX | SCNuMAX | 0 | UINTMAX_MAX |