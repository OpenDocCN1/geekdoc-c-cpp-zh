```
Class StringBad
{
private:
    char * str;
    int len;
    static int num_strings;
public:
    ...
};
```

![](bbox=[0.18, 0.29, 0.88, 0.58])

# Figure 12.1  A static data member.

By the way, Listing 12.1 uses the num_strings member as a convenient means of illustrating static data members and as a device to point out potential programming problems. In general, a string class doesn’t need such a member.

Take a look at the implementation of the class methods in Listing 12.2. Notice how it handles using a pointer and a static member.

# Listing 12.2  strngbad.cpp

```
// strngbad.cpp -- StringBad class methods
#include <cstring>                // string.h for some
#include "strngbad.h"
using std::cout;

// initializing static class member
int StringBad::num_strings = 0;

// class methods
```