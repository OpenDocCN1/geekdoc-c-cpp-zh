# Specifies that a following a, A, E, f, F, g, and G conversion specifier applies to an argument with type pointer to long double.

If a length modifier appears with any conversion specifier other than as specified, the behavior is undefined.

The conversion specifiers and their meanings are:

+   - d: Matches an optionally signed decimal integer, whose format is the same as expected for the subject sequence of the wcstol function with the value 10 for the base argument. The corresponding argument should be a pointer to signed integer.

+   - i: Matches an optionally signed integer, whose format is the same as expected for the subject sequence of the wcstol function with the value 0 for the base argument. The corresponding argument should be a pointer to signed integer.

+   - o: Matches an optionally octal integer, whose format is the same as expected for the subject sequence of the wcstol function with the value 8 for the base argument. The corresponding argument should be a pointer to unsigned integer.

+   - u: Matches an optionally signed decimal integer, whose format is the same as expected for the subject sequence of the wcstol function with the value 10 for the base argument. The corresponding argument should be a pointer to unsigned integer.

+   - x: Matches an optionally signed hexadecimal integer, whose format is the same as expected for the subject sequence of the wcstol function with the value 16 for the base argument. The corresponding argument should be a pointer to unsigned integer.

+   - a,e,f,g: Matches an optionally signed floating-point number, infinity, or NaN, whose format is as expected for the subject sequence of the wcstol function. The corresponding argument should be a pointer to floating.

+   - c: Matches a sequence of wide characters of exactly the number specified by the field width (1 if no field width is present in the directive).

If no 1 length modifier is present, characters from the input field are converted as if by repeated calls to the mrtomb function, with the conversion state described by an mbstate_t initialized to zero before the first character is converted. The corresponding argument shall be a pointer to the initial element of a character array large enough to accept the sequence. No null character is added.