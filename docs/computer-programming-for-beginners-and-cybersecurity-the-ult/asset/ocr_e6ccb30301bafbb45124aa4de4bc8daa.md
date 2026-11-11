```
}
```

When we define the derived class from the base class, the derived class will have access to the property and the function as well. Note that the property and function need to have the access modifier as either public or protected.

Derived class: Base Class

```
```cpp
{
// No need to define property1 and Function1, it will automatically inherit these.
}
```
```

Let’s now look at an example where we can use functions in derived classes.

Example 3: The following program is used to showcase how to use an inherited class with functions.

```
```cpp
#include <iostream>

using namespace std;

// Defining a simple Person class with a property of Name, ID, and also a function called Display.
class Person
{
public:
    string Name;
    int ID;
    void Display()
    {
        cout<<"ID "<<ID<<endl;
```
```