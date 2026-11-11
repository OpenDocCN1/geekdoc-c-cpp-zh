Table 15.1 Preprocessor Directives

| Directive | Function |
|---|---|
| #define | Defines a macro substitution |
| #undef | Undefines a macro |
| #include | Specifies the files to be included |
| #ifdef | Test for a macro definition |
| #endif | Specifies the end of #if. |
| #ifndef | Tests whether a macro is not defined. |
| #if | Test a compile-time condition |
| #else | Specifies alternatives when #if test fails. |

These directives can be divided into three categories which are as follows:

+   1. Macro substitution directives.
+   2. File inclusion directives.
+   3. Compiler control directives.

# 15.2 MACRO SUBSTITUTION LO 15.1

Macro substitution is a process where an identifier in a program is replaced by a predefined string composed of one or more tokens. The preprocessor accomplishes this task under the direction of #define statement. This statement, usually known as a macro definition (or simply a macro) takes the following general form:

```
```c
#define identifier string
```
```

If this statement is included in the program at the beginning, then the preprocessor replaces every occurrence of the identifier in the source code by the string. The keyword #define is written just as shown (starting from the first column) followed by the identifier and a string, with at least one blank space between them. Note that the definition is not terminated by a semicolon. The string may be any text, while the identifier must be a valid C name.

There are different forms of macro substitution. The most common forms are as follows:

+   1. Simple macro substitution.
+   2. Argumented macro substitution.
+   3. Nested macro substitution.

# Simple Macro Substitution

Simple string replacement is commonly used to define constants. Examples of definition of constants are as follows:

```
```c
#define COUNT 100
#define FALSE 0
#define SUBJECTS 6
#define PI 3.1415926
#define CAPITAL "DELHI"
```
```

Notice that we have written all macros (identifiers) in capitals. It is a convention to write all macros in capitals to identify them as symbolic constants. A definition, such as