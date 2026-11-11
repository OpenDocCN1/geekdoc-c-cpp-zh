counter part of if keyword in conditional statements. It provides the code which compiles when the associative #if condition fails. In other words, it provides an alternative compilation path.

compilation you may want to limit the levels of nesting.\n\nIf at lowest step in the ladder a #else preprocessor is present then the code associated with it compiles if all condition fails. Also like always #endif preprocessor is used to mark the end of the #elif block.

General form of using #else preprocessor is if condition.

```
statement1\nstatement2\n.\n.\n.\nstatementN.\n#else\nStatement N+1\nStatement N+2\n.\n.\n.\nStatement N+M.\n#endif
```

General form of using #elif preprocessor is as follows

```
#if condition\nstatement1\nstatement2\n.\n.\n.\nStatementN.\n#elseif\nstatementN+1\nstatementN+2\n.\n.\n.\nstatementN+M.\n.\n.\n.\n... A levels\n#else\nStatement N+M+A+1\nStatement N+M+A+1\n.\n.\n.\nStatement N+M+A+Z\n#endif
```

Following C source code shows the use of #else preprocessor.

```
#include <stdio.h>\n#include<conio.h>\n#define MACRO 1\nvoid main ()\n{\nclrscr();\n#if MACRO == 0\nprintf (”MACRO is false”);\n#else\nprintf (”MACRO is true”);\n#endif\ngetch();\n}
```

#elif preprocessor can be expanded to #else if and is used to construct a structure similar to if-else ladder. The structure it forms allows multiple compilation option and the control flow keeps on falling on next step in ladder till the conditions are evaluated to be false but if any condition evaluates to be true rest of the steps in ladder are bypassed on the same level. Also different levels can be produced using nesting of ladders. 8 levels in C89 and 63 levels in C99 are minimum supported but like always compilers support many more levels. Also for efficiency criteria and fast

The C source code given below shows the use of #elif preprocessor.

```
#include <stdio.h>\n#include<conio.h>\n#define MACRO 4\nvoid main ()\n{\nclrscr();\n#if MACRO == 0\nprintf (”MACRO has value 0”);\n#elseif MACRO == 1\nprintf (”MACRO has value 1”);\n#elseif MACRO == 2
```