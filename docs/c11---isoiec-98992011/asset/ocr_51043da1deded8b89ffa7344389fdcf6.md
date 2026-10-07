# 7.4 Character handling <ctype.h>

The header <ctype.h> declares several functions for classifying and mapping characters.(198) In all cases the argument is an int, the value of which shall be representable as an unsigned char or equal the value of marco EOF. If the argument has any other value, the behavior is undefined.

The behavior of these functions is affected by the current locale. Those functions that have locale-specific aspects are not in the "C" locale are noted below.

The term printing character refers to a member of a locale-specific set of characters, each of which occupies one positioning on a display device; the term control character refers to a member of a locale-specific set of characters that are not printing characters.(199) All letters and digits are printing characters.

**Forward references:** EOF (7.21.1), localization (7.21.1).

# 7.4.1 Character classification functions

The functions in this subclause return nonzero (true) if and only if the value of the argument c conforms to that in the description of the function.

# 7.4.1.1 The isnum function

Synopsis

```
#include <ctype.h>
int isnum(int c)
```

Description

The isnum function tests for any character for which isalpha or isdigit is true.

# 7.4.1.2 The isalpha function

Synopsis

```
#include <ctype.h>
int isalpha(int c)
```

Description

The isalpha function tests for any character for which isupper or islower is true, or any character that is one of a locale-specific set of alphabetic characters for which