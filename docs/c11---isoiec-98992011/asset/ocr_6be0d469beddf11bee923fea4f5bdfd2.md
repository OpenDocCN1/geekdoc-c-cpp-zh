ISO/IEC 9899:2011 (E)

L Specifies that a following a, A, e, E, f, g, or G conversion specifier applies to an argument with type pointer to long double.

If a length modifier appears with any conversion specifier other than specified above, the behavior is undefined.

+   2 The conversion specifiers and their meanings are:

+   d Matches an optionally signed decimal integer, whose format is the same as expected for the subject sequence of the wstol function with the value 10 for the base argument. The corresponding argument shall be a pointer to signed integer.

+   i Matches an optionally signed integer, whose format is the same as expected for the subject sequence of the wstol function with the value 0 for the base argument. The corresponding argument shall be a pointer to signed integer.

+   o Matches an optionally signed octal integer, whose format is the same as expected for the subject sequence of the wstol function with the value 8 for the base argument. The corresponding argument shall be a pointer to unsigned integer.

+   u Matches an optionally signed decimal integer, whose format is the same as expected for the subject sequence of the wstol function with the value 10 for the base argument. The corresponding argument shall be a pointer to unsigned integer.

+   x Matches an optionally signed hexadecimal integer, whose format is the same as expected for the subject sequence of the wstol function with the value 16 for the base argument. The corresponding argument shall be a pointer to unsigned integer.

+   a,e,f,g Matches an optionally signed floating-point number, infinity, or NaN, whose format is the same as expected for the subject sequence of the wstol function. The corresponding argument shall be a pointer to floating.

+   c Matches a sequence of wide characters of exactly the number specified by the field width (1 if no field width is present in the directive).

If no 1 length modifier is present, characters from the input field are converted as if by repeated calls to the wertomb function, with the conversion state described by an mbrstate_t object initialized to zero before the first character is converted. The corresponding argument shall be a pointer to an element large enough to accept the sequence. No null character added.

If an 1 length modifier is present, the corresponding argument shall be a