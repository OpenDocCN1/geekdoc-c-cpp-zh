The concept of virtual base class is to inherit one or more derived classes from a base class by using the virtual keyword. Note that when you create a virtual base class, you have only one copy of the base class members in memory. Moreover, such kind of inheritance, where a derived class is inherited from a virtual base class, is also called virtual inheritance. Listing 26 shows how to create and use a virtual base class (you can find the VirtualBase.cpp file on the CD in the Code\Chapter7 folder):

# ▶ **Listing 26: Creating and using a Virtual Base Class**

```
```cpp
#include<iostream.h>

class BaseA
{
public:
    int varA;
};

class BaseB: virtual public BaseA
{
public:
    int varB;
};

class BaseC: virtual public BaseA
{
public:
    int varC;
};

class DerivedClass : public BaseB, public BaseC
{
public:
    int varD;
};

int main()
{
    DerivedClass obj;
    obj.varA=10;      /*No ambiguity because only one copy of varA exists*/
    return 0;
}
```
```

In Listing 26, the BaseB and BaseC classes are inherited from the virtual class, BaseA by using the virtual keyword and class DerivedClass is inherited from both the BaseB and BaseC classes, so that only one copy of the varA variable of BaseA is inherited by the DerivedClass class. In this way, any reference to the varA variable through an object of the DerivedClass class does not lead to ambiguity.