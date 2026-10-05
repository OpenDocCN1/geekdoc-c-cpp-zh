```
if(typeid(obj1) == typeid(obj3))
cout << "obj1 and obj3 are the same type\n";

return 0;

```

```
// output
The type of i is: i
The type of f is: f*
The type of p is: char*
The type of obj1 is: myclass1
The type of obj2 is: myclass2
The types of i and j are the same
The types of i and f are not the same
obj1 and obj2 are of differing types
obj1 and obj3 are the same type
```

The most important use case for typeid occurs when it's argument is a pointer to a polymorphic base class. In this case, it will automatically return the type of the actual object pointed to, whether it is a base-class object or an object of a derived class.

Therefore by using typeid can determine at run-time the actual type of the polymorphic object that is being pointed to by a base-class pointer.

```
// An example that uses typeid on a polymorphic class hierarchy
#include <iostream>
#include <typeinfo>
using namespace std;

// Mammal is a polymorphic class
class Mammal
{
public:
    virtual bool lays_eggs() { return false; }
    };

class Cat: public Mammal {
};

class Platypus: public Mammal {
public:
    bool lays_eggs() { return true; }
    };

int main()
{
    Mammal *p, AnyMammal;
```