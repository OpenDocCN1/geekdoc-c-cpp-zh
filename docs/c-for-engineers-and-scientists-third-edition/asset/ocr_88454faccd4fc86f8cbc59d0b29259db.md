Although it might seem that the initialization of taxRate is global, it is not. After the definition is made, any other definition results in an error. Therefore, the actual definition of a static data member remains the responsibility of the class creator, and a compiler error occurs if this is omitted.

Figure 11.3 illustrates the storage shared by the static data member and the objects created in Program 11.4.

![](bbox=[0.218, 0.226, 0.778, 0.406])

**Figure 11.3** Sharing the static data member taxRate

In addition to static data members, static member functions can be created. These functions apply to a class as a whole instead of class objects and can access only static data members and other static data member functions of the class. Program 11.5 includes an example of a static data member function.

# Program 11.5

```
#include <iostream>
using namespace std;

// class declaration section
class Employee
{
private:
    static double taxRate;
    int idNum;
```