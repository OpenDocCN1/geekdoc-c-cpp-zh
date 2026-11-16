# TABLE 4-1 Fundamental Integer Data Types in ISO C89 (ANSI C)

| Signed Types | Typical Size | Typical Range |
| :--- | :--- | :--- |
| signed char | 8 bits | –128 to +127 |
| signed short int | 16 bits | –32,768 to + 32,767 |
| signed long int | 32 bits | –2,147,483,648 to +2,147,483,647 |
| signed long long int | 64 bits | –2^63 to +(2^63 – 1) |
| Unsigned Types | Typical Size | Typical Range |
| unsigned char | 8 bits | 0 to 255 |
| unsigned short int | 16 bits | 0 to 65,535 |
| unsigned long int | 32 bits | 0 to 4,294,967,295 |
| unsigned long long int | 64 bits | 0 to 18,446,744,073,709,551,615 |

Note: ANSI C does not specify the size or range of values for these integer types, but does require that their size be at least as large as listed above. When used without a modifier, the primitive data type int must not be smaller than a short int, nor larger than a long int. The long long integer types are common, but were not formally part of the C language until the ISO C99 standard of 1999.

# TABLE 4-2 Additional Integer Data Types in the ISO C99 Standard

| Signed Types | Specified Size | Specified Range (2's-complement) |
| :--- | :--- | :--- |
| int8_t | 8 bits | –128 to +127 |
| int16_t | 16 bits | –32,768 to + 32,767 |
| int32_t | 32 bits | –2,147,483,648 to +2,147,483,647 |
| int64_t | 64 bits | –9,223,372,036,854,775,808 to +9,223,372,036,854,775,807 |
| Unsigned Types | Specified Size | Specified Range |
| uint8_t | 8 bits | 0 to 255 |
| uint16_t | 16 bits | 0 to 65,535 |
| uint32_t | 32 bits | 0 to 4,294,967,295 |
| uint64_t | 64 bits | 0 to 18,446,744,073,709,551,615 |

Although the new C99 integer data types are an important addition for embedded applications, there are some compilers that still do not support them.1 In most situations, a simple workaround is to create your own header file containing typedef declarations of the new type names. As shown, the C99 pre-defined macro (_STDC_VERSION__) can be used to hide these declarations from a C99-compliant compiler.

```
#ifndef _STDC_VERSION_
typedef signed       char     int8_t ;
typedef signed       short int int16_t ;
```

1 C99 is not supported by the Microsoft Visual Studio 2010 C compiler.