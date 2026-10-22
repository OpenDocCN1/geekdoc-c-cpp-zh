Here’s another use. Suppose we place the line

```
#include "arrays.h"
```

at the head of a file. This results in SIZE being defined as 100. But placing

```
#define SIZE 10
#include "arrays.h"
```

at the head sets SIZE to 10. Here, SIZE is defined by the time the lines in arrays.h are processed, so the #define SIZE 100 line is skipped. You might do this, for example, to test a program using a smaller array size. When it works to your satisfaction, you can remove the #define SIZE 10 statement and recompile. That way, you never have to worry about modifying the header array itself.

The #ifndef directive is commonly used to prevent multiple inclusions of a file. That is, header files usually are set up along the following lines:

```
/* things.h */
#ifndef THINGS_H_
    #define THINGS_H_
    /* rest of include file */
#endif
```

Suppose this file somehow got included several times. The first time the preprocessor encounters this include file, THINGS_H_ is undefined, so the program proceeds to define THINGS_H_ and to process the rest of the file. The next time the preprocessor encounters this file, THINGS_H_ is defined, so the preprocessor skips the rest of the file.

Why would you include a file more than once? The most common reason is that many include files include other files, so you may include a file explicitly that another include file has already included. Why is this a problem? Some items that appear in include files, such as declarations of structure types, can appear only once in a file. The standard C header files use the #ifndef technique to avoid multiple inclusions. One problem is to make sure the identifier you are testing hasn’t been defined elsewhere. Vendors typically solve this by using the filename as the identifier, using uppercase, replacing periods with an underscore, and using an underscore (or, perhaps, two underscores) as a prefix and a suffix. If you check your stdio.h header file, for example, you’ll probably find something similar to this:

```
#ifndef _STDIO_H
#define _STDIO_H
// contents of file
#endif
```

You can do something similar. However, you should avoid using the underscore as a prefix because the standard says such usage is reserved. You wouldn’t want to accidentally define a macro that conflicts with something in the standard header files. Listing 16.10 uses #ifndef to provide multiple-inclusion protection for the header file from Listing 16.6.