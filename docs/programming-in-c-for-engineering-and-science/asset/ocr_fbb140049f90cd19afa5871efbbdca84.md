# 3.2.1 Fundamental Types

The most important fundamental data types provided in C++ are the following:¹

+   - **integers**: whole numbers and their negatives: of type `int`
+   - **integer variations**: types `short`, `long`, and `unsigned`
+   - **reals**: fractional numbers: of type `float`, `double`, or `long double`
+   - **characters**: letters, digits, symbols, and punctuation: of type `char`
+   - **booleans**: logical values `true` and `false`: of type `bool`

A value of one of these types is called a **literal**.² For example, 123, 0, and -15 are integer literals; -45.678 and 3.14159 are real literals; 'A', 'a', '0', and '$' are character literals; and true and false are boolean literals. We will now examine these types in more detail.

# 3.2.1.1 Integers

Integer literals are strings of digits that may be preceded by a - sign or a + sign. They are interpreted as

+   - **octal (base-eight)** integers if they begin with 0 and all digits are octal digits 0, 1, ..., 7;
+   - **hexadecimal (base-sixteen)** integers if they begin with 0x — the hexadecimal digits for ten, eleven, ..., fifteen are A, B, ..., F or their lowercase equivalents a, b, ..., f;
+   - **decimal (base-ten)** integers otherwise.

For example, the literal 345 has the decimal value 345₁₀ = 3 × 10² + 4 × 10¹ + 5 × 10⁰. However, the literal 0345 has the octal value 345₈ = 3 × 8² + 4 × 8¹ + 5 × 8⁰ = 229₁₀, and 0x345 has the hexadecimal value 345₁₆ = 3 × 16² + 4 × 16¹ + 5 × 16⁰ = 837₁₀. (See the text's website described in the preface for additional details about binary, octal, and hexadecimal number systems.)

Typically, `int` values are stored in 32 bits (= 4 bytes) and can range from −2³¹ (= −2147483648) through 2³¹ − 1 (= 2147483647). C++ also allows `int` declarations to be modified with one of the key words `short` or `long`:

+   - `short int` (or just `short`) values usually are usually stored in 16 bits (2 bytes) and can range from −2¹⁵ (= −32768) through 2¹⁵ − 1 (= 32767).
+   - `long int` (or just `long`) values are the same as `int` values in some versions of C++, while in others they are 64-bit values, ranging from −2⁶³ to 2⁶³ − 1.

¹ Other types are the `signed char` and `unsigned char` integer types, which are stored in one byte and thus can range from −2⁷ (= −128) through 2⁷ − 1 (= 127); the wide character type `wchar_t` for storing Unicode characters; `complex` for complex values; and the `void` type for an empty set of values.

² The word literal in computing refers to any value entered by a programmer that does not change during program execution—the string of characters you type is (literally) the value you get.