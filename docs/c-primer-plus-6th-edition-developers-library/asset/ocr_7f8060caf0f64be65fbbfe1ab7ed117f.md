```
chcount++;
}
```

This fragment echoes and counts nonspace characters.

# The goto Command

A goto statement causes program control to jump to a statement bearing the indicated label. A colon is used to separate a labeled statement from its label. Label names follow the rules for variable names. The labeled statement can come either before or after the goto.

# Form

```
goto label;
label : statement
```

# Example

```
top : ch = getchar();
    if (ch != 'y')
    goto top;
```

# Section V: The Standard ANSI C Library with C99 and C11 Additions

The ANSI C library classifies functions into several groups, with each group having an associated header file. This appendix gives you an overview of the library, listing the header files and briefly describing their associated functions. Some of these functions (for example, several I/O functions) are discussed in much greater detail in the text. More generally, for complete descriptions, consult the documentation for your implementation, or a reference manual, or try an online reference such as the following:http://www.acm.uiuc.edu/webmonkeys/book/c_guide/

# Diagnostics: assert.h

This header file defines assert() as a macro. Defining the macro identifier NDEBUG before including the assert.h header file deactivates the assert() macro. The expression used as an argument is typically a relational or logical expression that should be true at that point in the program if the program is functioning properly. Table RS.V.1 describes the assert() macro.