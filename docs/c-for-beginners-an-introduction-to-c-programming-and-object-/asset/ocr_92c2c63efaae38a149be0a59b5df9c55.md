**float.h**, etc. These are provided by the compiler software and hence these shall be placed inside pointed brackets and not quotes as follows:

```
```cpp
#include <stdlib.h>
#include <float.h>
```
```

# 2. Main Method

Main method serves as an entry point of the program. Every standalone C++ program must have a main method else the program will not know where to start executing from. Main method is essentially a function block enclosed within curly brackets ( { } ). The general syntax of a main method is as follows:

```
```cpp
int main ( )
{
    Statements...
    return 0;
}
```
```

Combining what we have learned in this section, here is a C++ program that does not do anything but compiles and executes properly.

```
```cpp
#include <iostream>
int main ( )
{
    //No meaningful statements, just a comment.
    return 0;
}
```
```

You may try compiling and executing the above program. The process will go ahead without a problem but you will not see