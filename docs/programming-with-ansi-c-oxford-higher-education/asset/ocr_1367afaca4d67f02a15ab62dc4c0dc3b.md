# PROGRAM 9.5 Access declaration to use a specific inherited member for a different purpose

```
//AccessDeclaration.cpp
#include <iostream>
using namespace std;

class Base
{
protected:
    int SpecialProtectedInt;
public:
    int SpecialInt;
    int NormalInt;
};

class Derived : private Base
{
protected:
    Base::SpecialProtectedInt;
    /* Making this protected integer specially available to the object of the derived class */
public:
    Base::SpecialInt;
    /* Making this integer specially available to the object of the derived class */
    // Using Base::SpecialInt;
    /* Newer way of writing the same */
    void SetSpecialProtectedIntOfBase()
    {
        SpecialProtectedInt = 10;
    }
};

void main()
{
    Derived DerivedObject;
    // DerivedObject.NormalInt = 10;
    /* This statement, if not commented, would not be compiled */
    DerivedObject.SpecialInt = 20;
    DerivedObject.SetSpecialProtectedIntOfBase();
}
```

# How the Program Works

The statement Base::SpecialInt; redefines the SpecialInt in the public access specifier header of the derived class, thus making it specially public. All other data will remain private. Thus, the NormalInt will still be private. Note that SpecialProtectedInt has also been redefined to remain protected in the derived class. Access declaration is a great facility; however, it has the following restrictions:

+   1. The access specifier cannot be modified to raise the status of the original access specifier. It means that if there is a private or protected member in the base, it cannot be redefined in the derived class as public.

+   2. The consequence of the previous statement is that a member with public access specification can be redefined with public or protected access, whereas the protected member can only be redefined as protected.