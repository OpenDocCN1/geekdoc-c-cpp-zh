```
int * pi;
void * pv;
pv = ar;          /* ok in C, C++ */
pi = pv;          /* ok in C, invalid in C++ */
pi = (int * ) pv; /* ok in C, C++ */
```

Another difference in C++ is that you can assign the address of a derived-class object to a base-class pointer, but that relates to features that don’t even exist in C.

# Boolean Types

In C++, the Boolean type is bool, and true and false are keywords. In C, the Boolean type is _Bool, but including the header file stdbool.h makes bool, true, and false available.

# Alternative Spellings

In C++, the alternative spellings of or for ||, and so on, are keywords. In C99 and C11, they are defined as macros, and you need to include iso646.h to make them available.

# Wide-Character Support

In C++, wchar_t is a built-in type, and wchar_t is a keyword. In C99 and C11, the wchar_t type is defined in several header files (stddef.h, stdlib.h, wchar.h, wctype.h). Similarly, char16_t and char32_t are C++11 keywords but are macros defined inuchar.h in C11.

C++ provides wide-character I/O support (wchar_t, char16_t, and char32_t) through the iostream header file, whereas C99 provides a completely different package of I/O support through the wchar.h header file.

# Complex Types

C++ supports complex types through a complex class provided by the complex header file. C has built-in complex types and supports them through the complex.h header file. The two approaches are quite different and are not compatible with one another. The C version reflects a greater concern with the needs and practices of the numerical computation community.

# Inline Functions

C99 has added inline function support, a feature C++ already had. However, the C99 implementation is more flexible. In C++, an inline function has internal linkage by default. If a C++ inline function appears in more than one file, it has to have the same definition, using the same tokens. For example, one file can’t have a definition using a type int parameter and another file have a definition using a type int32_t parameter, even if int32_t is a typedef for int. C, however, allows that arrangement. Also, C, as described in Chapter 15, allows a mixture of inline and external definitions that C++ doesn’t allow.