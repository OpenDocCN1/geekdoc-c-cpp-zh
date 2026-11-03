# Limit constants

The table below lists constants related to maximum and minimum numerical limits. Their values vary according to implementation. Where a value is given, in brackets, it indicates a minimum size for that constant – but larger values may, in fact, be imposed. Programs should not assume that any implementation-dependent constant will be of a particular value.

| Constant | Value |
|---|---|
| CHAR_BIT | number of bits in a char (8) |
| CHAR_MAX | maximum value of char (UCHAR_MAX or SCHAR_MAX) |
| CHAR_MIN | minimum value of char (zero or SCHAR_MIN) |
| INT_MAX | maximum value of int (+32,767) |
| INT_MIN | minimum value of int (-32,767) |
| LONG_MAX | maximum value of long (+2,147,483,647) |
| LONG_MIN | minimum value of long (-2,147,483,647) |
| SCHAR_MAX | maximum value of signed char (+127) |
| SCHAR_MIN | minimum value of signed char (-127) |
| SHRT_MAX | maximum value of short (+32,767) |
| SHRT_MIN | minimum value of short (-32,767) |
| UCHAR_MAX | maximum value of unsigned char (+255) |
| UINT_MAX | maximum value of unsigned int (+65,535) |
| ULONG_MAX | maximum value of unsigned long (+4,294,967,295) |
| USHRT_MAX | maximum value of unsigned short (+65,535) |