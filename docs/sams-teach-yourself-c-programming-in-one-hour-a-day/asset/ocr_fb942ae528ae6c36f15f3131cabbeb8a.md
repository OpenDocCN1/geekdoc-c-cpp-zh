```
#if ENGLAND == 1
#include "england.h"
#elif FRANCE == 1
#include "france.h"
#elif ITALY == 1
#include "italy.h"
#else
#include "usa.h"
#endif
```

Then, by using #define to define the appropriate symbolic constant, you can control which header is included during compilation.

# Using #if...#endif to Help Debug

Another common of #if...#endif is to include conditional debugging code in the program. You could define a DEBUG symbolic constant set to either 1 or 0. Throughout the program, you can insert debugging code as follows:

```
#if DEBUG == 1
debugging code here
#endif
```

During program development, if you define DEBUG as 1, the debugging code is included to help track any bugs. After the program works properly, you can redefine DEBUG as 0 and recompile the program without the debugging code.

The defined() operator is useful when you use conditional compilation directives. This operator tests to see whether a particular name is defined. Then, the expression

defined( NAME ) evaluates to TRUE or FALSE depending on whether NAME is defined. By using defined(), you can control compilation, based on previous definitions, without regard to the specific value of a name. Referring to the previous debugging code example, you could rewrite the #if...#endif section as follows:

```
#if defined( DEBUG )
debugging code here
#endif
```

You can also use defined() to assign a definition to a name only if it hasn’t been previously used. Using the NOT operator (! ) as follows:

```
#if !defined( TRUE )   /* if TRUE is not defined. */
#define TRUE 1
#endif
```