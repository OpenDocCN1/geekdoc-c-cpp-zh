# ISO/IEC 9899:2011 (E)

4 When preprocessing tokens are converted to tokens during translation phase 7, if a preprocessing token could be converted to either a keyword or an identifier, it is converted to a keyword.

# Implementation limits

5 As discussed in 5.2.4.1, an implementation may limit the number of significant initial characters in an identifier; the limit for an external name (an identifier that has external linkage) may be more restrictive than that for an internal name (a macro name or an identifier that does not have external linkage). The number of significant characters in an identifier is implementation-defined.

6 Any identifiers that differ in a significant character are different identifiers. If two identifiers differ only in nonsign characters, the behavior is undefined.

**Forward references:** universal character names (6.4.3), macro replacement (6.10.3).

# 6.4.2.2 Predefined identifiers

# Semantics

1 The identifier __func__ shall be implicitly declared by the translator as if, immediately following the opening brace of function definition, the declaration

```c\static char __func__[] = "function-name";
```nappeared, where function-name is the name of the lexically-enclosing function.⁷2)

2 This code is encoded as if the implicit had been written in the source character set and then translated into the execution character set as indicated in translation phase 5.

3 EXAMPLE Consider the code fragment:

```c\#include <stdio.h>
void myfunc(void)
{
    printf("%s\n", __func__);
    /* */
}
Each time the function is called, it will print to the standard output stream:

myfunc

**Forward references:** function definitions (6.9.1).

> 72) Since the name __func__ is reserved for any use by the implementation (7.1.3), if any other identifier is explicitly declared using the name __, the behavior is undefined.