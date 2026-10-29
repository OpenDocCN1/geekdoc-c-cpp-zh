is not defined to mean anything but merely put on a list. The important point is that you can use another directive to test whether DTIME_H has been defined and so test whether a section of code has already been processed. You can use any (nonkeyword) identifier in place of DTIME_H, but you will see that there are standard conventions for which identifier you should use.

The following directive tests to see whether DTIME_H has been defined:

```
#ifndef DTIME_H
```

If DTIME_H has already been defined, then everything between this directive and the first occurrence of the following directive is skipped:

```
#endif
```

An equivalent way to state this, which may clarify the way the directives are spelled, is the following: If DTIME_H is not defined, then the compiler processes everything up to the next #endif. The not is why there is an n in #ifndef. (This may lead you to wonder whether there is a #ifdef directive as well as a #ifndef directive. There is, and it has the obvious meaning, but we will have no occasion to use #ifdef.)

Now consider the following code:

```
#ifndef DTIME_H
#define DTIME_H
< a class definition >
#endif
```

If this code is in a file named dtime.h, then no matter how many times your program contains

```
#include "dtime.h"
```