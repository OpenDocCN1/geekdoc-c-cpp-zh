![](bbox=[0.163, 0.094, 0.226, 0.161])

If you have a source file containing some functions, creating a header file that contains the associated function prototypes is generally a good practice. Then you can name the header file the same as the source file, except with a different extension. In this example, you use the safestuff.h file to hold the prototype for the Safestuff.cpp file.

# Adding the header only once

Code::Blocks includes several lines in the header file by default. These lines create a symbol that tells the compiler whether a header file is already included in the source file so that the compiler doesn’t add it twice. Adding a header twice is an error because then you define the forward reference for a function twice. Here is what you see when you initially create a header file with Code::Blocks:

```
```cpp
#ifndef SAFESTUFF_H_INCLUDED
#define SAFESTUFF_H_INCLUDED
#endif // SAFESTUFF_H_INCLUDED
```
```

When you type the header code into Code::Blocks, type it between the #define SAFESTUFF_H_INCLUDED and #endif // SAFESTUFF_H_INCLUDED lines. The section “Using the Mysterious Header Wrappers,” later in this chapter, describes these automatic entries in detail.

# Using angle brackets or quotes

You may have noticed something about the code in Listing 7-3. When including the safestuff.h file, you don’t put it inside angle brackets, as with the #include <iostream> line. Instead, you put it inside quotes:

```
```cpp
#include "safestuff.h"
```
```

That’s because programmers for years have been fighting over the rules of where exactly on the hard drive to put the header files. The question is whether to put them in the same directory or folder as your project or to place them in a directory all by themselves.

![](bbox=[0.163, 0.771, 0.226, 0.837])

Regardless of where you put your header files, here is the rule for when to use quotes and when to use brackets: The compiler looks in several directories to find header files. And it can, possibly, look in the same directory as the source file. If you use angle brackets (that is, less-than and greater-than signs), as in #include <string>, the compiler doesn’t look in the same directory as the source file. But if you use double quotes, as in #include "safestuff.h", the compiler first looks in the same directory as the source file. And if the compiler doesn’t find the header file there, it looks in the remaining directories, as it would with angle brackets.