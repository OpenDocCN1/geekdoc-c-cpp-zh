```
Base class2
{
Public or protected:
Property2;
Fucntion2;
}
```

Then when we define the derived class from both of the base classes, the derived class will have access to the property and the function of both classes.

```
Derived class: Base Class1, Base Class2
{
// No need to define property1, property2, and Function1, Function2
it will automatically inherit these.
}
```

Again note that the property and function need to have the access modifier as either public or protected. Let’s look at an example of multiple derived classes.

Example 5: The following program is used to showcase how to use multiple derived classes.

```
#include <iostream>

using namespace std;

// Defining the first base class of Person
class Person
{
public:
```