
## CHAPTER 11 Separate Compilation and Namespaces

If DTIME_H has already been defined, everything between this directive and the first occurrence of the following directive is skipped:

```cpp
#endif
```

An equivalent way to state this, which may clarify the way the directives are spelled, is the following: If DTIME_H is not defined, the compiler processes everything up to the next #ifdef. The not is why there is an n in #ifndef. (This may lead you to wonder whether there is a #ifdef directive as well as a #ifndef directive. There is, and it has the obvious meaning, but we will have no occasion to use #ifdef.)

```cpp
#ifndef DTIME_H
#define DTIME_H
<class definition>
#endif
```

If this code is in a file named dtime.h, no matter how many times your program contains

```cpp
#include "dtime.h"
```

the class will be defined only one time.
The first time

```cpp
#include "dtime.h"
```

is processed, the flag DTIME_H is defined and the class is defined. Now, suppose the compiler encounters

```cpp
#include "dtime.h"
```

When the include directive is processed this second time, the directive

```cpp
#ifndef DTIME_H
```

says to skip everything to
so the class is not defined again.

```cpp
#endif
```

In Display 11.4 we have rewritten the header file dtime.h shown in Display 11.1, but this time we used these to prevent multiple definitions. With the version of dtime.h shown in Display 11.4, if a file contains the include directive more than once, the class DigitalTime will still be defined only once:

```cpp
#include "dtime.h"
```

You may use other identifier in place of DTIME_H, but the normal convention is to use the name in all uppercase letters with the underscore instead of the period. You should follow this so that others can easily read your code and that you do not have to remember the flag name. This way the flag name is determined automatically and there is nothing arbitrary to remember.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_513_0.png)

These same directives can be used to skip code in files other than header files, but we will not have occasion to use these directives except in header files.

### Display 11.4 Avoiding Multiple Definitions of a Class

```cpp
// This is the header file dtime.h. This is the interface for the class
// DigitalTime, Values of this type are times of day. The values are
// input and output in 24-hour notation, as in 9:30 for 9:30 AM and
// 14:45 for 2:45 PM.

#ifndef DTIME_H
#define DTIME_H

#include <iostream>
using namespace std;

class DigitalTime
{
<The definition of the class DigitalTime is the same as in Display 11.1.>
};
#endif //DTIME_H
```

> #ifndef
You can avoid multiple definitions of a class (or anything else) using #ifndef in the header file (interface file), as illustrated in Display 11.4. If the file is included more than once, only one of the definitions will be used.

TIP: Defining Other Libraries
You need not define a class in order to use separate compilation. If you have a collection of related functions that you want to make into a library of your own design, you can place the function declarations (prototypes) and accompanying comments in a header file and the function definitions in an implementation file, just as we outlined for classes. After that, you can use this library in your programs the same way you would use a class that you placed in separate files.

### Self-Test Exercises

1. Suppose that you are defining a class and that you then want to use this class in a program. You want to separate the class and program parts into separate files as described in this chapter. State whether of the following should be placed in the interface file, implementation file, or application file.
   - a. The class definition
   - b. The declaration for a function that is to serve as a class operation but that is neither a member nor a friend of the class
   - c. The declaration for an overloaded operator that is to serve as a class operation but that is neither a member nor a friend of the class
   - d. The definition for a function that is to serve as a class operation but that is neither a member nor a friend of the class
   - e. The definition for a friend function that is to serve as a class operation
   - f. The definition for a member function
   - g. The definition for an overloaded operator that is to serve as a class operation but that is neither a member nor a friend of the class
   - h. The definition for an overloaded operator that is to serve as a class operation but that is a friend of the class
   - i. The main function of your program
2. Which of the following files has a name that ends in .h: the interface file for a class, the implementation file, or the application file that uses the class?
3. When you define a class in separate files, there is an interface file and an implementation file. Which of these needs to be compiled? (Both? Neither?) Only one? If so, which one?
4. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class. If any, needs to be recompiled: the interface file, the implementation file, or the application file?
5. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class. If any, needs to be recompiled: the interface file, the implementation file, or the application file?
6. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class. If any, needs to be recompiled: the interface file, the implementation file, or the application file?
7. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class. If any, needs to be recompiled: the interface file, the implementation file, or the application file?
8. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class. If any, needs to be recompiled: the interface file, the implementation file, or the application file?
9. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class. If any, needs to be recompiled: the interface file, the implementation file, or the application file?
10. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class. If any, needs to be recompiled: the interface file, the implementation file, or the application file?

### 11.2 Namespaces

> What's in a name? That by other name would smell as sweet.
> WILLIAM SHAKESPEARE, Romeo and Juliet

When a program uses different classes and functions written by different programmers there is a possibility that two programmers will use the same name for different things. A namespace is a collection of name definitions, such as class definitions and variable declarations. A namespace can be turned on and off so that when some of its names would otherwise conflict with other names.

A good way to see why you might want to include this using directive is to think about why you might want to not include it. If you do not include this using directive for the namespace, then you can define cin and count to have some other meaning than their standard. differently from the standard versions. Their standard is in the std namespace; without the using directive (or something like it), as far as your code is concerned, the only definitions of cin and count are whatever definitions you give them.

Every bit of code you write; if you do not place the code in some specific namespace, the code is known as the global namespace. So we have not placed any code we wrote in any namespace and so all our code is in the global namespace. The global namespace does not have a using directive because you are always using the global namespace. You could say there is an implicit automatic using directive that says you are using the global namespace.

Note that you can use more than one namespace in the same program. For example, we are always using the global namespace and we are usually the std namespace. What happens if a name is defined in two namespaces and you are using both namespaces?
