
Input white-space characters (as specified by the ispace function) are skipped, unless the specification includes a [, c, or n specifier.²84

An input item is read from the stream, unless the specification includes an n specifier. An input item is defined as the longest sequence of input characters which does not exceed any specified field width and which is, a prefix of, a matching sequence. The first character, if any, after the input item is unread. If the length of the input item is zero, the execution of the directive fails; this condition is a matching failure unless end-of-file, an encoding error, or a read error prevented input from the stream, in which case it is an input failure.

Except in the case of a % specifier, the input item (or, in the case of a %n directive, the count of input characters) is converted to a type appropriate to the conversion specifier. If the input item is not a matching sequence, the execution of the directive fails; unless assignment suppression was indicated by a *, the result of the conversion is placed in the object pointed to by the first argument that has not already received a result. If this object does not have an appropriate type, or if the result of the conversion cannot be represented in the object, the behavior is undefined.

The modifiers and their meanings are:

- + hh
Specifies that a d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to signed char or unsigned char.

- + h
Specifies that a d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to short int or unsigned short int.

- + l (ell)
Specifies that a d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to long int or unsigned long int; that a following a, E, e, F, g, or G conversion specifier applies to an argument with type pointer to double; or that a following c, s, or [ conversion specifier applies to an argument with type pointer to wchar_t.

- + ll (ell-ell)
Specifies that a d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to long long int or unsigned long long int.

284 These white-space characters are not counted against a specified field width.

285 fscanf pushes back at most one character onto the input stream. Therefore, some sequences are acceptable to strtod, strtol, etc., are unacceptable to fscanf.

- + j
Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to intmax_t or uintmax_t.

- + z
Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to size_t or the corresponding signed integer type.

- + t
Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to ptrdiff_t or the corresponding unsigned integer type.

- + L
Specifies that a following a, E, f, F, g, or G conversion specifier applies to an argument with type pointer to long double.

If a length modifier appears with any conversion specifier other than as specified, the behavior is undefined.

The conversion specifiers and their meanings are:

- + d Matches an optionally signed decimal integer, whose format is the same as expected for the subject sequence of the strtol function with the value 10 for the base argument. The corresponding argument shall be a pointer to signed integer.

- + i Matches an optionally signed integer, whose format is the same as expected for the subject sequence of the strtol function with the value 0 for the base argument. The corresponding argument shall be a pointer to signed integer.

- + o Matches an optionally signed octal integer, whose format is the same as expected for the subject sequence of the strtol function with the value 8 for the base argument. The corresponding argument should be a pointer to unsigned integer.

- + u Matches an optionally signed decimal integer, whose format is the same as expected for the subject sequence of the strtol function with the value 10 for the base argument. The corresponding argument shall be a pointer to unsigned integer.

- + x Matches an optionally signed hexadecimal integer, whose format is the same as expected for the subject sequence of the strtol function with the value 16 for the base argument. The corresponding argument shall be a pointer to unsigned integer.

- + a,e,f,g Matches an optionally signed floating-point number, infinity, or NaN, whose format is the same as expected for the subject sequence of the strtod function. The corresponding argument shall be a pointer to float.

Matches a sequence of characters of exactly the number specified by the field width (1 if no field width is present in the directive).^286

If no l length modifier is present, the corresponding argument shall be a pointer to the initial element of a character array large enough to accept the sequence. No null character is added.

If an l length modifier is present, the input shall be a sequence of multibyte characters that begins in the initial shift state. Each multibyte character in the sequence is converted to a wide character as by a call to the mbstowc function, with the conversion state described by an mbstate_t object initialized to zero before the first multibyte character is converted. The corresponding argument shall be a pointer to the initial element of an array of wchar_t large enough to accept the resulting sequence of wide characters. No null wide character is added.

Matches a sequence of non-white-space characters.^286

If no l length modifier is present, the corresponding argument shall be a pointer to the initial element of a character array large enough to accept the sequence. No null character is added.

If an l length modifier is present, the input shall be a sequence of multibyte characters that begins in the initial shift state. Each multibyte character in the sequence is converted to a wide character as by a call to the mbstowc function, with the conversion state described by an mbstate_t object initialized to zero before the first multibyte character is converted. The corresponding argument shall be a pointer to the initial element of an array of wchar_t large enough to accept the resulting sequence of wide characters. No null wide character is added.

Matches a sequence of characters from a set (scancet).^286

If no l length modifier is present, the corresponding argument shall be a pointer to the initial element of a character array large enough to accept the sequence and a null character, which is added.

If an l length modifier is present, the input shall be a sequence of multibyte characters that begins in the initial shift state. Each multibyte character is converted to a wide character as by a call to the mbstowc function, with the conversion state described by an mbstate_t object initialized to zero[336]

before the first multibyte character is converted. The corresponding argument shall be a pointer to the initial element of an array of wchar_t large enough to accept the resulting sequence of wide characters and a null wide character, which is added.

The conversion specifier includes all subsequent characters in the format string, up to and including the matching bracket (]). The characters between the brackets (scanlist) compose the scanet, unless the character after the left bracket is a circumflex (^), in which case the scanet contains all characters that do not appear in the scanet between the circumflex and the right bracket. If the conversion specifier begins with [] or [^], the right bracket character is in the scanlist and the next right bracket character is the one that ends the specification; otherwise the first following bracket character is the one that ends the specification. If a - character is in the scanet and not the first, nor the first character is ^, nor the last character, the behavior is implementation-defined.

Matches an implementation-defined set of sequences, which should be the same as the set of sequences that may be produced by the % conversion of the fprintf function. The corresponding argument shall be a pointer to pointer to void. The input item is converted to a pointer value in an implementation-defined manner. If the input is a value converted earlier during the same program execution, the pointer shall compare equal to that value; otherwise the behavior of the % conversion is undefined.

No input is consumed. The corresponding argument shall be a pointer to signed integer which is to be written the number of characters read from the input stream by this call to the fscanf function. Execution of a %n directive does not increment the assignment count returned at the completion of execution of the fscanf function. No argument is converted, but one is. If the conversion specification includes an assignment-suppressing character or a field width, the behavior is undefined.

Matches a single % character; no conversion or assignment occurs. The complete conversion specification is invalid, shall be %.

- If a conversion specification is invalid, the behavior is undefined.¹²⁷)

- + The conversion specifiers A, E, F, G, and X are also valid and behave the same as, respectively, a, e, f, g, and x.

> ²⁸⁷) See “future library directions” (7.31.11).
