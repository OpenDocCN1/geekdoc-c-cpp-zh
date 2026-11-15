# ## C.2.2.3 Standard file sections

Standard sections in the library header and C source files are summarised below.

# ## C.2.2.3.1 Standard pre-processor directives

The contents of every header (* .h) file must be enclosed in a standard pre-processor directive (below). LibraryFileName is the name of the library file, e.g. str for ajstr.h/c:

```
```c
#ifdef __cplusplus
extern "C"
{
#endif

#ifndef ajLibraryFileName_h
#define ajLibraryFileName_h

/* Everything else goes here */

#endif
#ifdef __cplusplus
}
#endif
```
```

# ## C.2.2.3.2 Standard library documentation header

A standard documentation header (see Appendix D, Code documentation standards) should go at the top of every library source (* .c) file.

# ## C.2.2.3.3 Inclusion of header files

Any files that are required for compilation are included before any code proper. Inclusions of system files are given before local files. You should never use nested includes.

# ## C.2.2.3.4 Definition of constants

These include #define and enum statements and should be given in a block and documented where necessary.

# ## C.2.2.3.5 Definition of global variables

Global variables follow constants in the library source (* .c) file. Global variables should normally be commented if their function is not obvious from their name. They should be avoided wherever possible.

# ## C.2.2.3.6 Definition of datatypes

Any unions and C data structures (objects) that are private (and should be declared as static) are given in the library source (* .c) file. Any public (external) unions and structures are given in the library header (* .h) file. All datatypes should be defined in the EMBOS style (Section C.8, ‘Structures and unions’). All public datatypes must be documented in a standard way (see Appendix D, Code documentation standards). Such documentation is not required for private structures and unions, although it is recommended.