"Polymorphism, Dynamic Typing, and Dynamic Binding," discusses extensively.

Table 4.1 summarizes the basic data types and qualifiers.

# Table 4.1. Basic Data Types

| Type | Constant Examples | NSLog chars |
|---|---|---|n| char | 'a', '\n' | \c |
| short int | | \hi, \hx, \ho |
| unsigned short int | 12L, -97, 0xFFFE, 0177 | \hu, \hx, \ho |
| unsigned int | 12u, 100U, 0xFFU | \u, %x, %o |
| long int | 12L, -2001, 0xFFFFFF | \li, \lx, \lo |
| unsigned long int | 12UL, 0xEEUL | \lu, \lx, \lo |
| long int | 0xE5e5e5e5LL, 5001 | \lli, \lx, \lo |
| unsigned long long int | 12ULL, 0xFFULL | \llu, \lx, \llo |
| float | 12.34f, 3.1e-5f, 0x1p10, 0x1P-1 | %f, %e, %g, %a |
| double | 12.34, 3.1e-5, 0.1p3 | %f, %e, %g, %a |
| long double | 12.34DL, 3.1e-51 | %Lf, %Le, %Lg |
| id | nil | %p |

# Note

In the table, a leading zero in front of an integer constant indicates the constant is in octal (base 8) notation, whereas a leading 0x (or 0X) indicates it is in hexadecimal (base 16) notation. A number written as 0x1p3 represents a hexadecimal floating constant. Don't worry about these formats, they're summarized in the table here for completeness. Further, suffixes such as f, 1 (L), u (U), and 11 (LL) can also be used to explicitly express constants as float's, long's, unsigned, and long long, respectively.