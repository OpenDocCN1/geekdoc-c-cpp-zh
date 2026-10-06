# ISO/IEC 14882:2017(E)

Identifiers that are keywords or operators in C++ shall not be defined as macros in C++ standard library headers.171

D.5, Standard library headers, describes the effects of using the name.h (C header) form in C++ program.172

Annex K of the standard describes a large number of functions, with associated types and macros, "promote safer, more secure programming" than many of the traditional C headers. The names of the functions have a suffix of _: most of them provide the same behavior as the C library with the unsigned name, if namely an additional argument which is the size of the result. If any C++ header is included, it is implementation-defined whether any of names are declared in the global namespace. (One of them is declared in std).

Table 18 lists the Annex K names that may be defined in some header. These names are also subject to the restrictions of20.5.4.3.2.

# Table 18 — Standard Annex K names

| abort_handler_s | strncat_s | vsscanf_s |
| astime_s | memccpy_s | vsprintf_s |
| bsearch_s | memmove_s | strtok_s | vwscanf_s |
| constraint_handler_s | memset_s | swprintf_s | wctomb_s |
| ctime_s | printf_s | wscanf_s | wcscat_s |
| errno_s | SIZE_MAX | tmpfile_s | wcscpy_s |
| fopen_s | rsize_t | TMP_MAX | wcsnc_s |
| fprint_s | scanf_s | vsprintf_s | wcscanf_s |
| freopen_s | set_constraint_handler_s | vscanf_s | wctorbs_s |
| scancf_s | | vsprintf_s | wctstok_s |
| vsprintf_s | snprintf_s | vprintf_s | wctstbs_s |
| vsscanf_s | | vprintf_s | wctombs_s |
| getenv_s | scancf_s | vsscanf_s | wmemmove_s |
| gmtime_s | strcat_s | vsprintf_s | wprintf_s |
| ignore_handler_s | strcpy_s | vsscanf_s | |
| L_tmpnam_s | strerror_s | vsnprintf_s | |
| locale_s | strrlen_s | vsscanf_s | |
| shartowcs_s | strlen_s | vsprintf_s |

# 20.5.1.3 Freanding implementations [compliance]

Two implementations are defined: hosted and freestanding (4.1). For a hosted implementation, the document describes the set of available headers.

A freestanding implementation has an implementation-defined set of headers. This set shall include at least the headers shown in Table 19.

The supplied version of the header <stddef> shall declare at least the functions abort, atxit, quick_exit_, and quick_exit (21.5). The other headers in this table shall meet the same requirements as a hosted implementation.

171 In particular, using the standard header <iso64.h> or <iso66> has no effect.
172 The "b" headers dump all names into the global namespace, whereas the newer forms keep their names in namespace std. Therefore, the newer are the preferred forms for all uses except for C++ programs which are intended to be strict with C.

20.5.1.3 ©ISO/IEC 2017 – All rights reserved 456