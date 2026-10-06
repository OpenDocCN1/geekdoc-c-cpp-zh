```
santaMonica();
malibu();
...
}
```

With this approach, name clashes are more likely to occur. If the compiler complains about an ambiguous name (e.g., two classes with the same name defined in two different namespaces), we can always qualify the identifier with the name of the namespace when referring to it.

# The C++ Preprocessor

The C++ preprocessor is a program that converts a .cpp source file containing # directives (such as #include, #ifdef, and #endif) into a source file that contains no directives. The preprocessor performs textual operations on the source file, such as conditional compilation, file inclusion, and macro expansion. Normally, the preprocessor is invoked automatically by the compiler, but most systems still offer a way to invoke it alone (often through a -E /E compiler option).

+   - #include the contents of the file specified within angle brackets (<>) or double quotes(""), depending on the header file is installed at a standard location or is part of the current project. The file name may contain ... and / (which Windows compilers correctly interpret as the directory separator). For example:
#include "../shared/globaldefs.h"
- #define defines a macro. Occurrences of the macro appearing after the #define directive are replaced with the macro's definition. For example, the directive
#define PI 3.14159265359

tells the preprocessor to replace all future occurrences of the token PI in the current compilation unit with the token 3.14159265359. To avoid clashes with variable and class names, it is common practice to give macros all-uppercase names. It is possible to define macros that take arguments:
#define SQUARE(x) ((x) * (x))

In the macro body, it is good style to surround all occurrences of the parameters with parentheses, as well as the entire body, to avoid problems with operator precedence. After all, we want 7 * SQUARE(2 + 3) to expand 7 ((2 + 3), (2 + 3)), not to 7 + 2 + 3 + 2 + 3.

C++ normally allows us to define macros on the command line, using

![](bbox=[0.0, 0.9, 1.0, 1.0])