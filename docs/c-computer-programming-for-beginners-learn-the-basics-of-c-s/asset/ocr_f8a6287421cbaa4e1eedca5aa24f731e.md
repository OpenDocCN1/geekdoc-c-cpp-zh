The following result is produced when you execute the code shown above.

Variable num for s1: 6

Variable num for s2: 6

A member function can also be declared as static. These functions will be accessed static variables only. Moreover, static functions can exist even before the creation of the object.

Take a look at the following example to get a better understanding of these static functions.

```
using System;
namespace StaticVarApplication
{
    class StaticVar
    {
        public static int num;
        public void count()
        {
            num++;
        }
        public static int getNum()
        {
            return num;
        }
    }
```