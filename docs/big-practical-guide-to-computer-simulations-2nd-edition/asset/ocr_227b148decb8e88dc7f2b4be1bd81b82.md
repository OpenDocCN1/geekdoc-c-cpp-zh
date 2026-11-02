deleted via the #undef directive.

When scanning the code, the preprocessor just replaces literally every occurrence of a macro by its definition. If you have, for example, the expression 2.0*PI*omega in your code, the preprocessor will convert it into 2.0*3.1415926536*omega. You can use macros also in the definition of other macros. But macros are not replaced in strings, i.e. printf("PI"); will print PI and not 3.1415926536 when the program is run.

It is possible to test for the (non)existence of macros using the #ifdef and #ifndef directives. This allows for conditional compiling or for platform-independent code, such as in

```
```
#ifdef UNIX
...
#endif
#ifdef MSDOS
...
#endif
```
```

Please note that it is possible to supply definitions of macros to the compiler via the -D option, e.g. cc -o program program.c -DUNIX=1. If a macro is used only for conditional #ifdef/#ifndef statements, an assignment like =1 can be omitted, i.e. -DUNIX is sufficient.

When programs are divided into several modules, or when library functions are used, the definitions of data types and functions are provided in header files (.h files), as mentioned above. It is important that each header file should be read by the compiler only once for each source code file, otherwise declarations will appear twice and the compiler will complain. When projects become more complex, many header files have to be managed, and it may become difficult to avoid multiple scanning of some header files. This can be prevented automatically by this simple construction using macros:

```
```
/** example .h file: myfile.h  **/

#ifndef _MYFILE_H_
#define _MYFILE_H_

  .... (rest of .h file)
  (may contain other #include directives)

#endif /* _MYFILE_H_ */
```
```