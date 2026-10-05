# Description

2 The **isograph** function tests for any printing character except space (' ').

# 7.4.1.7 The islower function

Synopsis

```
#include <ctype.h>
int islower(int c);
```

# Description

2 The **islower** function tests for any character that is a lowercase letter or is one of a locale-specific set of characters for which none of **iscntrl**, **isdigit**, **ispunct**, or **isspace** is true. In the "C" locale, **islower** returns true only for the lowercase letters (as defined in 5.2.1).

# 7.4.1.8 The isprint function

Synopsis

```
#include <ctype.h>
int isprint(int c);
```

# Description

2 The **isprint** function tests for any printing character including space (' ').

# 7.4.1.9 The isispunct function

Synopsis

```
#include <ctype.h>
int ispunct(int c);
```

# Description

2 The **ispunct** function tests for any printing character that is one of a locale-specific set of characters for which neither **isspace** nor **isalnum** is true. In the "C" locale, **ispunct** returns true for every printing character for which neither **isspace** nor **isalnum** is true.

# 7.4.1.10 The isspace function

Synopsis

```
#include <ctype.h>
int isspace(int c);
```

# Description

2 The **isspace** function tests for any character that is a standard white-space character or is one of a locale-specific set of characters for which **isalnum** is false. The standard