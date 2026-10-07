# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

+   c Matches a sequence of characters of exactly the number specified by the field width (1 if no field width is present in the directive).286

If no 1 length modifier is present, the corresponding argument shall be a pointer to the initial element of a character array large enough to accept the sequence. No null character is added.

If an 1 length modifier is present, the input shall be a sequence of multibyte characters that begins in the initial shift state. Each multibyte character is converted to a wide character as by a call to the mbrtow function, with the conversion state described by an mbstate_t object initialized to zero before the first multibyte character is converted. The corresponding argument shall be a pointer to the initial element of an array of wchar_t large enough to accept the resulting sequence of wide characters. No null wide character is added.

+   s Matches a sequence of non-white-space characters.286

If no 1 length modifier is present, the corresponding argument shall be a pointer to the initial element of a character array large enough to accept the sequence and a terminating null character, which will be added automatically.

If an 1 length modifier is present, the input shall be a sequence of multibyte characters that begins in the initial shift state. Each multibyte character is converted to a wide character as by a call to the mbrtowc function, with the conversion state described by an mbstate_t object initialized to zero before the first multibyte character is converted. The corresponding argument shall be a pointer to the initial element of an array of wchar_t large enough to accept the sequence and the terminating null character, which will be added automatically.

+   [ Matches a nonempty sequence of characters from a set of expected characters (the scanset).286

If no 1 length modifier is present, the corresponding argument shall be a pointer to the initial element of a character array large enough to accept the sequence and a terminating null character, which will be added automatically.

If an 1 length modifier is present, the input shall be a sequence of multibyte characters that begins in the initial shift state. Each multibyte character is converted to a wide character as by a call to the mbrtowc function, with the conversion state described by an mbstate_t object initialized to zero

> 286) Special provisions are made for multibyte characters in the matching rules used by c, and for conversion specifies — the extent of the input field is determined by a byte-by-byte basis. The resulting field is not necessarily a sequence of characters in the shift state.

# 320

# Library

# §71.216.2