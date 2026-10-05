+   The argument in an instance of the integer-constant macros is not a decimal, octal, or it has a value that exceeds the limits for the corresponding type (72.20.4).

+   A byte input/output function is applied to a wide-oriented stream, or a wide character input/output function is applied to a byte-oriented stream (72.21.2).

+   Is used of any portion of a file beyond the most recent wide character written to a wide-oriented stream (72.21.2).

+   The value of a pointer to a FILE object is used after the associated file is closed (72.21.3).

+   The stream for the fflush function points to an input stream or to update an stream in which the most recent operation was input (72.21.5.2).

+   The string pointed to by the mode argument in a call to the fopen function does not exactly match one of the specified character sequences (72.21.5.3).

+   An output operation on an update stream is followed by an input operation without an intervening call to the fflush function or a file positioning function, or an input operation on an update stream is followed by an output operation with an intervening call to a file positioning function (72.21.5.3).

+   An attempt is made to use the contents of the array that was supplied in a call to the setvbuf function (72.21.5.6).

+   There are insufficient arguments for the format in a call to one of the formatted input/output functions, or an argument does not have an appropriate type (72.21.6.1, 72.21.6.2, 72.29.2.1, 72.29.2.2).

+   The format in a call to one of the formatted input/output functions or to the strftime function is not a valid multibyte character sequence that begins and ends in its initial shift state (72.21.6.1, 72.21.6.2, 72.37.5, 72.29.2.1, 72.29.5.1).

+   In a call to one of the formatted output functions, a precision appears with a conversion specifier other than those described (72.21.6.1, 72.29.2.1).

+   A conversion specification for a formatted output function uses an asterisk to denote an argument-supplied field width or precision, but the corresponding is not provided (72.21.6.1, 72.29.2.1).

+   A conversion specification for a formatted output function uses a # or flag with a conversion specifier other than those described (72.21.6.1, 72.29.2.1).

+   A conversion specification for one of the formatted input/output functions uses a length modifier with a conversion specifier other than those described (72.21.6.1, 72.29.2.1, 72.29.2.2).