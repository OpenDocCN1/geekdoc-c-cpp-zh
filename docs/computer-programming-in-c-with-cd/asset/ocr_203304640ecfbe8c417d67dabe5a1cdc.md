copies of the same base class. Listing 25 shows how to use the `::` operator to solve the problem of ambiguity, which arises when the derived class has multiple copies of the same base class (you can find the UsingSRO2.cpp file on the CD in the `Code\\Chapter7` folder):

# Listing 25: Using the :: Operator to Create a Single Copy of a Base class

```
```cpp
#include<iostream.h>

class BaseA
{
public:
    int varA;
};
class BaseB: public BaseA
{
public:
    int varB;
};
class BaseC: public BaseA
{
public:
    int varC;
};
class DerivedClass: public BaseB, public BaseC
{
public:
    int varD;
};

int main()
{
    DerivedClass obj;
    obj.BaseB::varA=10;
    obj.BaseC::varA=50;
    return 0;
}
```
```

In Listing 25, an object, obj, of the DerivedClass class can access the varA variable of the BaseB and BaseC classes with the help of the :: operator.

# Implementing the Concept of Virtual Base Classes

We know that a problem arises for the C++ compiler when a base class is inherited by multiple classes, and then a derived class is inherited from these multiple classes. The whole process creates multiple copies of base class members in the derived class. This problem can be solved in two ways, by using :: operator (as discussed in the earlier section), and by using the concept of virtual base class.