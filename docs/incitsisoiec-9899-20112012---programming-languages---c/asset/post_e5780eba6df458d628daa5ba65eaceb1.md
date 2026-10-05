
An s conversion specifier is encountered by one of the formatted output functions, (unless a specifier is specified that does not require termination) (72.61.1, 72.29.2).

An n conversion specifier for one of the formatted input/output functions includes any flags, an assignment-suppressing character, a field width, or a precision (72.61.1, 72.61.2, 72.29.1, 72.29.2).

A % conversion specifier is encountered by one of the formatted input/output functions, but the complete conversion specification is not exactly % (72.61.1, 72.61.2, 72.29.1, 72.29.2).

An invalid conversion specification is found in the format for one of the formatted input/output functions, the strftime or wcsftime function (72.61.1, 72.61.2, 72.37.3, 72.29.1, 72.29.2, 72.29.5).

- The number of characters or wide characters transmitted by a formatted output function (or written to an array, or would have been written to an array) is greater than INT_MAX (72.61.1, 72.29.1).
- The number of items assigned by a formatted input function is greater than INT_MAX (72.61.2, 72.29.2).
- The result of a conversion by one of the formatted input functions cannot be represented in the corresponding object, or the receiving object does not have an appropriate type (72.61.2, 72.29.2).
- A c, s, or [ conversion specifier is encountered by one of the formatted input functions, and the array pointed to by the corresponding argument is not large enough to accept the input sequence (and a null terminator if the conversion specifier is s or }) (72.61.2, 72.29.2).
- A c, s, or [ conversion specifier with a # is encountered by one of the formatted input functions, but the input is not a valid multibyte character sequence that begins in the initial state (72.61.2, 72.29.2).
- The item part for a % conversion by one of the formatted input functions is not a value converted early during the same program execution (72.61.2, 72.29.2).
- The vfprintf, vsprintf, vprintf, vsprintf, vsprintf, vscanf, vfprintf, vsscanf, vwcanf, vscanf, and vwcsf function is called with an improperly initialized va_list argument, or the argument is used (other than in an invocation of va_end) after the function returns (72.61.8, 72.61.9, 72.61.10, 72.61.11, 72.61.12, 72.61.13, 72.61.14, 72.29.5, 72.29.6, 72.29.7, 72.29.8, 72.29.10).
- The contents of the array supplied in a call to the fgets or fget function are used after a read error (72.71.2, 72.29.3).
- The file position indicator for a binary stream is used after a call to the ungetc function where its value was zero before the call (72.1.7.10).
- The file position indicator for a stream is used after an error occurred during a call to the read or write function (72.1.8.1, 72.1.8.2).
- A partial element read by a call to the read function is used (72.1.8.1).
- The fseek function is called for a text stream with a nonzero offset and either the offset was not returned by a previous successful call to the ftell function on a stream associated with the same file or whence is SEEK_SET (72.1.9.2).
- The fsetpos function is called to set a position that was not returned by a previous successful call to the fgetpos function on a stream associated with the same file (72.1.9.3).
- A non-null pointer returned by a call to the calloc, malloc, or realloc function with a zero requested size is used to access an object (72.22.3).
- The value of a pointer that refers to space deallocated by a call to the free or realloc function is used (72.22.3).
- The alignment requested of the aligned_alloc function is not valid or not supported by the implementation, or the size requested is not an integral multiple of the alignment (72.2.3.1).
- The pointer argument to the free or realloc function does not match a pointer earlier returned by a memory management function, or the space has been deallocated by a call to free or realloc (72.2.3.3, 72.2.3.5).
- The value of the object allocated by the malloc function is used (72.2.3.4).
- The value of any bytes in a new object allocated by the realloc function beyond the size of the old object is used (72.2.3.5).
- The program calls the exit or quick_exit function more than once, or calls both functions (72.2.4.4, 72.2.4.7).
- During the call to a function registered with the atexit or at_quick_exit function, a call is made to the longjmp function that would terminate the call to the registered function (72.2.4.4, 72.2.4.7).
- The string set up by the getenv or strerror function is modified by the program (72.2.4.6, 72.4.6.2).
- A signal is raised while the quick_exit function is executing (72.2.4.7).
- A command is executed through the system function in a way that is documented as causing termination or some other form of undefined behavior (72.2.4.8).

![](img/b1371b4bc75a631228eb4aa5fac6584.png)

The string set up by the getenv or strerror function is modified by the program (72.2.4.6, 72.4.6.2).

A signal is raised while the quick_exit function is executing (72.2.4.7).

A command is executed through the system function in a way that is documented as causing termination or some other form of undefined behavior (72.2.4.8).

A searching or sorting function is called with an invalid pointer, even if the length is zero (72.24.1).

The current state is used by multibyte conversion (72.29.5).

The value of an argument of type wint_t is neither equal to EOF nor representable as wchar_t (30.1).

The iswtype function is called using a different LC_TYPE category from the one in effect for the call to wctype (30.2.2).

The towrans function is called using a different LC_TYPE category from the one in effect for the call to wctrans (30.3.2.1).
