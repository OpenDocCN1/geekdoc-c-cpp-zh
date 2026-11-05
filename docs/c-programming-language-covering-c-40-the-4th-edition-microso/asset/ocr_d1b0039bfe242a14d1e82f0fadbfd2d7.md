# 4.1.5 Integral Types

C# supports nine integral types: sbyte, byte, short, ushort, int, uint, long, ulong, and char. The integral types have the following sizes and ranges of values:

+   - The sbyte type represents signed 8-bit integers with values between −128 and 127.
+   - The byte type represents unsigned 8-bit integers with values between 0 and 255.
+   - The short type represents signed 16-bit integers with values between −32768 and 32767.
+   - The ushort type represents unsigned 16-bit integers with values between 0 and 65535.
+   - The int type represents signed 32-bit integers with values between −2147483648 and 2147483647.
+   - The uint type represents unsigned 32-bit integers with values between 0 and 4294967295.
+   - The long type represents signed 64-bit integers with values between −9223372036854775808 and 9223372036854775807.
+   - The ulong type represents unsigned 64-bit integers with values between 0 and 18446744073709551615.
+   - The char type represents unsigned 16-bit integers with values between 0 and 65535. The set of possible values for the char type corresponds to the Unicode character set. Although char has the same representation as ushort, not all operations permitted on one type are permitted on the other.

> > **JESSE LIBERTY** I have to confess that with the power of modern PCs, and the greater cost of programmer time relative to the cost of memory, I tend to use int for just about any integral (nonfractional) value and double for any fractional value. All the rest, I pretty much ignore.

The integral-type unary and binary operators always operate with signed 32-bit precision, unsigned 32-bit precision, signed 64-bit precision, or unsigned 64-bit precision:

+   - For the unary + and ~ operators, the operand is converted to type T, where T is the first of int, uint, long, and ulong that can fully represent all possible values of the operand. The operation is then performed using the precision of type T, and the type of the result is T.
+   - For the unary – operator, the operand is converted to type T, where T is the first of int and long that can fully represent all possible values of the operand. The operation is then performed using the precision of type T, and the type of the result is T.