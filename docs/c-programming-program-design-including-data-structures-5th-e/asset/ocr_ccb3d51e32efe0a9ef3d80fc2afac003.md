```
```cpp
class myException
{
public:
    myException()
    {
        message = "Something is wrong!";
    }

    myException(string str)
    {
        message = str;
    }

    string what()
    {
        return message;
    }

private:
    string message;
};
```
```

> > **NOTE**  
> > In the definition of the class `myException`, the constructors can also be written as follows:
> >
> > ```cpp
> > myException() : message ("Something is wrong!"){
> > myException(string str) : message (str){}
> > ```

The program in Example 15-17 illustrates how exceptions thrown in a function get processed in the calling environment.

# ### EXAMPLE 15-17

```
```cpp
// Processing exceptions thrown by a function in the calling
// environment.

#include <iostream>
#include "myException.h"

using namespace std;

void functionA() throw (myException);
void functionB() throw (myException);
void functionC() throw (myException);

int main()
{
    try
    {
        functionA();
    }
```
```