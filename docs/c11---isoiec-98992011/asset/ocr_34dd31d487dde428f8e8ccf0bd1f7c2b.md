# ISO/IEC 9899:2011 (E)

+   An s conversion specifier is encountered by one of the formatted functions, and the argument is missing the null terminator (unless a precision is specified that does not require null termination) (7.21.6.1, 7.29.2.1).

+   An n conversion specification for one of the formatted input/output functions includes any flags, an assignment-signing character, a field width, or a precision (7.21.6.2, 7.21.6.2, 7.29.2.1, 7.29.2.2).

+   A % conversion specifier is encountered by one of the formatted input/output functions, but the complete conversion specification is not valid %% (7.21.6.1, 7.21.6.2, 7.29.2.1, 7.29.2.2).

An invalid conversion specifier is found in the format for one of the formatted input/output functions, or the strftime wctime function (7.21.6.1, 7.21.6.2, 7.27.3.5, 7.29.2.1, 7.29.2.2, 7.29.5.1).

The number of characters or wide characters translated by a formatted output function (or to an array, which would have been written to an array) is greater than INT_MAX (7.21.6.1, 7.29.2.1).

The number of input items assigned by a formatted input function is greater than INT_MAX (7.21.6.2, 7.29.2.2).

The result of a conversion encountered by one of the formatted input functions cannot be represented in the corresponding object, or the receiving object does not have an appropriate type (7.21.6.2, 7.29.2.2).

+   A s, or [ conversion specifier is encountered by one of the formatted functions, and the argument pointed to the corresponding argument is not large enough to accept the input sequence (and a null terminator if the conversion specifier is s or } (7.21.6.2, 7.29.2.2).

+   A c, or [ conversion specifier with an l qualifier is encountered by one of the formatted input functions, and the input is not a valid multibyte character sequence that begins in the input shift (7.21.6.2, 7.29.2.2).

The item for a %p conversion by one of the formatted input functions is not a value converted early during the program execution (7.21.6.2, 7.29.2.2).

The vprintf, vsscanf, vprintf, vscanf, vsprintf, vprintf, vfwprintf, vwprintf, vswprintf, v vwprintf, or vsprintf is called with an properly initialized va_list argument, or the argument is used (other than in an invocation of va_end) after the function returns (7.21.6.8, 7.21.6.9, 7.21.6.10, 7.21.6.11, 7.21.6.12, 7.21.6.13, 7.21.6.14, 7.29.2.5, 7.29.2.7, 7.29.2.10).

The contents of the array supplied to a fgets or getws function are used after a read error (7.21.2.2, 7.29.3.2).