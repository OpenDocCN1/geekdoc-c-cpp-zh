338) The first wide character, if any, after the input item remains. If the length of the input item is zero, the execution of the directive fails; this condition is a matching failure unless end-of-file, an encoding error, or a read prevented input from the stream, in which case it is an input failure.

Except in the case of a % specifier, the input item (or, in the case of a %n directive, the count of input characters) is converted to a type appropriate to the conversion specifier. If the input item is not a matching sequence, the execution of the directive fails: this condition is a matching failure. Unless assignment superscript was indicated by a *, the result of the conversion is placed in the object pointed to by the first argument following the format argument that has not already received a conversion result. If this object does not have an appropriate type, or if the result of the conversion cannot be represented in the object, the behavior is undefined.

The length modifiers and their means are:

+   hh  Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to signed char or unsigned char.

+   h  Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to short int or unsigned short

+   l (ell) Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to long int or unsigned long int; that a following a, A, E, f, F, or G conversion specifier applies to an argument with type pointer to double; or that a following c, s, or [ conversion specifier applies to an argument with type pointer to wchar_t.

+   11 (ell-ell) Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to long long int or unsigned long long int.

+   j  Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to intmax_t or uintmax_t.

+   z  Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to size_t or the corresponding signed integer type.

+   t  Specifies that a following d, i, o, u, x, or n conversion specifier applies to an argument with type pointer to ptrdiff_t or the corresponding signed integer type.

> 338) fwscanf pushes back most one wide character onto the input stream. Therefore, some sequences that are acceptable to wcstop, wcstol, etc., are unacceptable to fwscanf.