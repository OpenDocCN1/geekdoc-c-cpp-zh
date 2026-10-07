
## J.3.7 Arrays and pointers

- The result of converting a pointer to an integer or vice versa (6.3.2.3).
- The size of the result of subtracting two pointers to elements of the same array (6.5.6).

## J.3.8 Hints

- The extent to which suggestions made by using the register storage-class specifier are effective (6.7.1).
- The extent to which suggestions made by using the inline function specifier are effective (6.7.4).

## J.3.9 Structures, enumerations, and bit-fields

- Whether a “plain” int bit-field is treated as a signed int bit-field or as an unsigned int bit-field (6.7.2, 6.7.1).
- Allowable bit-field types other than _Bool, signed int, and unsigned int (6.7.2.1).
- Whether atomic types are permitted for bit-fields (6.7.2.1).
- Whether a bit-field can straddle a storage-unit boundary (6.7.2.1).
- The order of allocation of bit-fields within a unit (6.7.2.1).
- The alignment of non-bit-field members of structures (6.7.2.1). This should present no problem unless binary data written by one implementation is read by another.
- The integer type compatible with each enumerated type (6.7.2.2).

## J.3.10 Qualifiers

- What constitutes an access to an object that has volatile-qualified type (6.7.3).

## J.3.11 Preprocessing directives

- The locations within #pragma directives where header name preprocessing tokens are recognized (6.4, 6.7).
- How sequences in forms of header names are mapped to headers or external source file names (6.4.7).
- Whether the value of a constant character in a constant expression that controls conditional inclusion matches the value of the same character in the execution character set (6.10.1).
- Whether the value of a single-character constant in a constant expression that controls conditional inclusion may have a negative value (6.10.1).
- The places that are searched for an included <> <>, and how the places are specified or the header is identified (6.10.2).
- How the named source file is searched for in an included "" delimited header (6.10.2).
- The method by which preprocessing tokens (possibly resulting from macro expansion) in a #include directive are combined into a header (6.10.2).
- The nesting limit for #include processing (6.10.2).
- Whether the # operator inserts a \ character that begins a universal name in a character or string literal (6.10.3.2).
- The behavior on each recognized non-STDC #pragma directive (6.10.6).
- The definitions for __DATE__ and __TIME__ when respectively, the date and time of translation are not available (6.10.8.1).

## J.3.12 Library functions

- Any library facilities available to a freestanding program, other than the minimal set required by clause 4 (5.1.2.1).
- The format of the diagnostic printed by the assert macro (7.2.1.1).
- The representation of the floating-point status flags stored by the febgetexcept_ (7.6.2.2).
- Whether the feraiseexcept raises the "inexact" floating-point exception in addition to the "overflow" or "underflow" floating-point exception (7.6.2.3).
- Strings other than "C" and "" may be passed as the second argument to the setlocale function (7.11.1.1).
- The types defined for float_t when the value of the FLT_EVAL_METHOD macro is less than 0 (7.12).
- Domain errors for the mathematics functions, other than those required by this Standard (7.12.1).
- The values returned by the mathematics functions on domain errors (7.12.1).
- The values returned by the mathematics functions on underflow errors, errno is set to the value of the macro ERANGE, and the "underflow" floating-point exception is raised when errno_ERCEPT is nonzero (7.12.1).
- Whether a domain error or zero is returned when an fmod function has a second argument of zero (7.12.10.1).
- Whether a domain error or zero is returned when a remainder function has a second argument of zero (7.12.10.2).
- The base-2 logarithm using the remquo functions in reducing the quotient (7.12.10.3).
- Whether a domain error or zero is returned when remquo function has a second argument of zero (7.12.10.3).
- Whether the equivalent of signal (sig, SIGDFL); is executed prior to the call of signal handler, and if not, the blocking of signals is performed (7.14.1.1).
- The null pointer constant to the macro expands (7.19).
- Whether the last line of a text stream requires a terminating-line character (7.21.2).
- Whether space characters that are written out to a text stream immediately before a new-line character appear when read (7.21.2).
- The number of null characters that may be appended to data written to binary stream (7.21.2).
- Whether the file position indicator of append-mode stream is initially positioned at the beginning or end of the file (7.21.3).
- Whether a write on a text stream causes the associated file to be truncated beyond point (7.21.3).
- The characteristics of file buffering (7.21.3).
- Whether a zero-length file actually exists (7.21.3).
- The rules for composing valid file names (7.21.3).
- Whether the same file can be simultaneously open multiple times (7.21.3).
- The nature and choice of encodings for multibyte characters in files (7.21.3).
- The effect of remove function on an open file (7.21.4.1).
- The effect if a file with the new name exists prior to a call of rename function (7.21.4.2).
- Whether an open temporary file is removed upon abnormal termination (7.21.4.3).
- Which changes of mode are permitted (if any), and under what circumstances (7.21.5.4).
- The style used to print an infinity or NaN, and the meaning of any n-char or n-wchar sequence printed for NaN (7.21.6.1, 7.29.2.1).
- The output for %p conversion in the sprintf or fprintf function (7.21.6.1, 7.29.2.1).
- The interpretation of a - character that is neither the first nor the last character, nor the second where ^ character is the first, in the scanlist for [] conversion in the fscanf and sscanf function (7.21.6.2, 7.29.2.1).
- The set of sequences matched by %p conversion and the interpretation of the corresponding item in the fscanf and swscanf function (7.21.6.2, 7.29.2.2).
- The value to which the errno is set by the fgetpos, fsetpos and ftell functions failure (7.21.9.1, 7.21.9.3, 7.9.4).
- The meaning of any n-char or n-wchar sequence in a string representing a NaN that is converted by the strtof, strtold, strtol, wcstol, wcstof, or wcstol function (7.21.1.3, 7.29.4.1).
- Whether or not the strtof, strtold, strtol, wcstol, wcstof, or wcstol function sets errno to ERANGE when underflow occurs (7.21.1.3, 7.29.4.1).
- Whether calloc, malloc, and realloc functions return a null pointer or a pointer to an allocated object when the size requested is zero (72.22.3).
- Whether open streams with unbuffered buffered data are flushed, open streams are closed, or temporary files are removed when the abort or _Exit is called (72.22.4.1, 72.22.4.5).
- The termination status returned to the host environment by the abort, _Exit, or quick_exit function (72.22.4.1, 72.22.4.4, 72.22.4.5, 72.22.4.7).
- The value returned by the system when its argument is not a null pointer (72.22.4.8).
