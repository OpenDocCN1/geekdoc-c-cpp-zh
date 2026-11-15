Most of these are welcome additions. In EMBOSS, passing whole structures around is deprecated because it can be wasteful of stack memory and rather slow. Each EMBOSS object (C data structure) has a pointer defined for it which should be used for referencing (see below).

If you need to write system-dependent code then try to put such functions in a separate header file to isolate them as much as possible. The AJAX library file ajsys.c may well be suitable for such code. Remember that your code will need to work under many operating systems, e.g. Linux, Windows, MacOSX, etc.

# C.4 Use of the pre-processor

The contents of every header (*.h) file must be enclosed in the pre-processor directives shown above.

The pre-processor can be used for:

+   - System-dependent code (but see the ajsys corollary above.)
+   - Commenting out code with #if 0
+   - Conditionals arising from system limits
+   - Definitions (#define); but consider enum or static const instead (see below).

An example of a conditional arising from system limits:

```
#include <limits.h>

#if INT_MAX > UCHAR_MAX
...
#else
#error "need int wider than char"
#endif
```

# C.4.1 Constants

For constants, consider using enum and variables instead of #define, which is rarely visible in debuggers. For example:

```
enum { Red = 0xF00, Blue = 0x0F0, Green = 0x00F };
static const float pi = 3.14159265358;
```

# C.4.2 Macros

Macros should avoid side effects. If possible, mention each argument exactly once. Put parentheses around all arguments. When the macro is an expression, put parentheses around the whole macro body. If the macro is the inline expansion of some function then capitalise the name and precede it with M:

```
#define MAJFUBAR (X) \
(save = (X), \
```