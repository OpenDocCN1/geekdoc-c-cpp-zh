The argument maxSize indicates the limiting number of wide characters.

The argument format is a wide string and the conversion specifiers are replaced by corresponding sequences of wide characters.

The return value indicates the number of wide characters.

# Returns

If the total number of resulting wide characters including the terminating null character is not more than maxSize, the wcsftime function returns the number of wide characters placed into the array pointed by s not including the terminating wide character. Otherwise, zero is returned and the contents of the array are indeterminate.

# 7.29.6 Extended multibyte/wide character conversion utilities

The header <wchar.h> declares an extended set of functions for conversion between multibyte characters and wide characters.

Most of the functions — those that are listed as “restartable”, 7.29.6.3 and 7.29.6.4 — take as a last argument pointer to an object of type mbstate_t that is used to describe the current conversion state from a particular multibyte sequence to (the reverse) under the rules of a particular setting for the LC_CTYPE category of the current locale.

On entry, each function takes the described conversion state (either internal or pointed to by an argument) as argument. The conversion state described by the referenced object is altered as needed to track the shift state, and the position within a multibyte character, for the associated multibyte character sequence.

> 348 Thus, a particular mbstate_t object can be used, for example, with both the mbrtowc and mbrtowcs functions as long as they are used to step sequentially through the same multibyte character string.