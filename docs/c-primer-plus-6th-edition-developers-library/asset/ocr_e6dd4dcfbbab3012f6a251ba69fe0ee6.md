# The #ifdef, #else, and #endif Directives

A short example will clarify what conditional compilation does. Consider the following:

```
#ifdef MAVIS
    #include "horse.h"  // gets done if MAVIS is #defined
    #define STABLES  5
#else
    #include "cow.h"  // gets done if MAVIS isn't #defined
    #define STABLES  15
#endif
```

Here we’ve used the indentation allowed by newer implementations and by the ANSI standard. If you have an older implementation, you might have to move all the directives, or at least the # symbols (see the next example), to flush left:

```
#ifdef MAVIS
#  include "horse.h"  /* gets done if MAVIS is #defined  */
#  define STABLES  5
#else
#  include "cow.h"  /* gets done if MAVIS isn't #defined */
#  define STABLES  15
#endif
```

The #ifdef directive says that if the following identifier (MAVIS) has been defined by the preprocessor, follow all the directives and compile all the C code up to the next #else or #endif, whichever comes first. If there is an #else, everything from the #else to the #endif is done if the identifier isn’t defined.

The form #ifdef #else is much like that of the C if else. The main difference is that the preprocessor doesn’t recognize the braces ({}) method of marking a block, so it uses the #else (if any) and the #endif (which must be present) to mark blocks of directives. These conditional structures can be nested. You can use these directives to mark blocks of C statements, too, as Listing 16.9 illustrates.

# Listing 16.9 The ifdef.c Program

```
/* ifdef.c -- uses conditional compilation */
#include <stdio.h>
#define JUST_CHECKING
#define LIMIT 4

int main(void)
{
    int i;
    int total = 0;

    for (i = 1; i <= LIMIT; i++)
```