x = 4.56
m = 100
y = 1.23
m = 200
n = 300

![](bbox=[0.138, 0.228, 0.203, 0.275])

> **NOTE:** *Understand how the data members are qualified when they are accessed.*

Program 16.5 uses functions in a namespace scope.

# Program 16.5 Using Functions in Namespace Scope

```
```cpp
#include <iostream>

using namespace std;

namespace Functions
{
    int divide(int x,int y)        // definition
    {
        return(x/y);
    }
    int prod(int x,int y);         // declaration only
}

int Functions:: prod(int x,int y)  // qualified
{
    return(x*y);
}
int main()
```
```