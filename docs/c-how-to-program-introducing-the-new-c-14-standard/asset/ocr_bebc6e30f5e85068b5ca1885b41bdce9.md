```
```cpp
// Text-printing program.
```
```

each begin with `//`, indicating that the remainder of each line is a **comment**. You insert comments to *document* your programs and to help other people read and understand them. Comments do not cause the computer to perform any action when the program is run—they’re *ignored* by the C++ compiler and do *not* cause any machine-language object code to be generated. The comment `Text-printing program` describes the purpose of the program. A comment beginning with `//` is called a **single-line comment** because it terminates at the end of the current line. You also may use comments containing one or more lines enclosed in `/*` and `*/`, as in

```
```cpp
/*
 * Fig. 2.1: fig02_01.cpp
 * Text-printing program. */
```
```

![](bbox=[0.12, 0.65, 0.19, 0.704])

# Good Programming Practice 2.1

*Every program should begin with a comment that describes the purpose of the program.*

# `#include` *Preprocessing Directive*

Line 3