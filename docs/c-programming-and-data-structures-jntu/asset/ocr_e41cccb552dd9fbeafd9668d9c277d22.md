+   - 2. Argumented macro substitution.
+   - 3. Nested macro substitution.

# Defining Macro

Simple string replacement is commonly used to define constants. Examples of definition of constants are:

| #define | COUNT | 100 |
| #define | FALSE | 0 |
| #define | SUBJECTS | 6 |
| #define | PI | 3.1415926 |
| #define | CAPITAL | "DELHI" |

Notice that we have written all macros (identifiers) in capitals. It is a convention to write all macros in capitals to identify them as symbolic constants.

# Undefining a Macro

A defined macro can be undefined, using the statement

```
#undef identifier
```

This is useful when we want to restrict the definition only to a particular part of the program.

# File Inclusion

An external file containing functions or macro definitions can be included as a part of a program so that we need not rewrite those functions or macro definitions. This is achieved by the preprocessor directive

```
#include "filename"
```

where filename is the name of the file containing the required definitions or functions. At this point, the preprocessor inserts the entire contents of filename into the source code of the program. When the filename is included within the double quotation marks, the search for the file is made first in the current directory and then in the standard directories. Alternatively this directive can take the form #include <filename> without double quotation marks. In this case, the file is searched only in the standard directories. Nesting of included files is allowed. That is, an included file can include other files. However, a file cannot include itself. If an included file is not found, an error is reported and compilation is terminated. Let use assume that we have created the following three files:

```
#include <filename>
```

| SYNTAX.C | contains syntax definitions. |
| STAT.C | contains statistical functions. |
| TEST.C | contains test functions. |