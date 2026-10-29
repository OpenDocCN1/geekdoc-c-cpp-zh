In Display 11.4 we have rewritten the header file dtime.h shown in Display 11.1, but this time we used these directives to prevent multiple definitions. With the version of dtime.h shown in Display 11.4, if a file contains the following #include directive more than once, the class DigitalTime will still be defined only once:

#include "dtime.h"

You may use some other identifier in place of DTIME_H, but the normal convention is to use the name of the file written in all uppercase letters with the underscore used in place of the period. You should follow this convention so that others can more easily read your code and so that you do not have to remember the flag name. This way the flag name is determined automatically and there is nothing arbitrary to remember.

These same directives can be used to skip over code in files other than header files, but we will not have occasion to use these directives except in header files.

#ifndef
You can avoid multiple definitions of a class (or anything else) by using #ifndef in the header file (interface file), as illustrated in Display 11.4. If the file is included more than once, only one of the definitions included will be used.

# Display 11.4 Avoiding Multiple Definitions of a Class

```
1 //This is the header file dtime.h. This is the interface for the class DigitalTime.
2 //Values of this type are times of day. The values are input and output in
3 //24-hour notation, as in 9:30 for 9:30 AM and 14:45 for 2:45 PM.
4
5 #ifndef DTIME_H
6 #define DTIME_H
7
8 #include <iostream>
9 using namespace std;
10
11 class DigitalTime
12 {
13     <The definition of the class DigitalTime is the same as in Display 11.1.>
14
15 };
16
17 #endif //DTIME_H
```