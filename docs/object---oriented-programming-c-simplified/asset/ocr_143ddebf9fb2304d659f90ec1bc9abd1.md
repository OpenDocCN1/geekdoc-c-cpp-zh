![](bbox=[0.147, 0.137, 0.857, 0.256])

![](bbox=[0.149, 0.268, 0.856, 0.384])

**EXPLANATION** : The function show_ele displays array element at given index. It takes both array arr and idx as its argument. If idx is within the limit 0 and 5 we display the array element as arr[idx] else we throw an exception “Array index out of bound”. As function show_ele may throw an exception it is put inside the try block. The exception thrown is caught by the catch block and handled.

# 14.5 EXCEPTION HANDLING WITH CLASS

Until now we have been doing exception handling without using class. We can use exception handling with class too. Even we can throw objects as exception of user defined class types. For throwing an exception of say demo class type within the try block we may write

throw demo( );

See few programs given below :

```
/* PROG 14.7 EXCEPTION HANDLING WITH SINGLE CLASS */

#include <iostream.h>
class demo
{
};
void main( )
{
        try
        {
                throw demo( );
        }
        catch(demo d)
```