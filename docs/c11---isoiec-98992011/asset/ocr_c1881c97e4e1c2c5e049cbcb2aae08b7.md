# 7.30 Wide character classification and mapping utilities <wctype.h>

# 7.31 Introduction

+   1 The header <wctype.h> defines one macro, and declares three data types and many functions. 352)

+   2 The types declared are
nnwint_t
described in 7.29.1;

wctrans_t
which is a scale type that can hold values which represent locale-specific character mappings; and

+   wctype_t
which is a scale type that can hold values which represent locale-specific character classifications.

+   3 The macro defined is WEOF (described in 7.29.1).

+   4 The functions declared are grouped as follows:
— Functions that provide wide character classification;
— Extensible functions that provide wide character case mapping;
— Extensible functions that provide wide character mapping.

+   5 For all functions described in this subclass that accept an argument of type wint_t, the value should be representable as a wchar_t or equal the value of the macro WEOF. If this argument has any other value, the behavior is undefined.

+   6 The behavior of these functions is affected by the LC_CTYPE category of the current locale.

> 352) See “future library directions” (7.31.17).