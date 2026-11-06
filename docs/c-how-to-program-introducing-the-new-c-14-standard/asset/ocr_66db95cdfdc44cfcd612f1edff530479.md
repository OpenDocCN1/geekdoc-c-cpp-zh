# Section E.4 `#define` Preprocessing  
Directive: Macros

+   - A macro is an operation defined in a `#define` preprocessing directive. Macros may be defined with or without arguments.
+   - The replacement text for a macro or symbolic constant is any text remaining on the line after the identifier (and, if any, the macro argument list) in the `#define` directive. If the replacement text for a macro or symbolic constant is too long to fit on one line, a backslash (`\`) is placed at the end of the line, indicating that the replacement text continues on the next line.
+   - Symbolic constants and macros can be discarded using the `#undef` preprocessing directive. Directive `#undef` “undefines” the symbolic constant or macro name.
+   - The scope of a symbolic constant or macro is from its definition until it is either undefined with `#undef` or the end of the file is reached.