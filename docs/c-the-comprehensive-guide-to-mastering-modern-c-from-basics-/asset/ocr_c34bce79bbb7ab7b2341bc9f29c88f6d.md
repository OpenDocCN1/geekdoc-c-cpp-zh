# 23.7.4 Overloading Variants

All possibilities of using custom suffixes have in common that they are defined by operator"". Then follow the differences:

+   - Type  nThe return type is always the one that the literal should ultimately have. Both built-in types and user-defined types are possible.

+   - Type operator ""_x(const char*)  nThe const char* form without length parameters raw strings. A sequence of digits like 1234_x is passed to operator ""_x(const char*) as a sequence of four characters and the terminating '\\0' character. Note that this does not refer to string literals, even if the argument is const char*: Raw means that the sequence of digits is not passed to the operator preprocessed. Because there are no quotation marks around the literal in the source code, you can only parse numeric literals this way. While you can write 234_x or 9.87_x in the source code, the compiler will complain about hello_x without quotation marks, as it meanwhile classified this as an identifier token, not as a literal.

+   - Type operator ""_x(unsigned long long)  nThe operator ""_x(unsigned double)  nPreprocessed (cooked) numeric literals are processed with the parameters unsigned long long and long double. Thus, 4847_x would result in a single call to operator ""_x (unsigned long long) with the decimal number 4847.