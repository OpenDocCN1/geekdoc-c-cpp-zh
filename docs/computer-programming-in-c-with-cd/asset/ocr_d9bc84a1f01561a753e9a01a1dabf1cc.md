```
```cpp
public:
    int varC;
...
};
class DerivedClass: public BaseB, public BaseC
{
    public:
        int varD;
    ...
};
int main()
{
    DerivedClass obj;
    obj.varA=10;
    return 0;
}
```
```

The preceding code snippet displays an error because the reference to the varA variable in the obj object is ambiguous. The ambiguity arises because the DerivedClass class inherits two copies of the varA variable, one from the BaseB class and another from the BaseC class.

Now, let’s describe how to resolve the ambiguities that arise in case of multiple inheritance. The first ambiguity can be resolved in the following two ways:

+   - Overriding the base class function in the derived class
+   - Using the Scope resolution operator (::)

The second ambiguity, again, can be solved in two ways, as follows:

+   - Using the Scope resolution operator (::)
+   - Implementing the concept of virtual base classes

Let’s describe these solutions in detail, one by one, in the following sections:

# ■ Overriding Base Class Functions in the Derived Class

The problem of ambiguity that arises in multiple inheritance when two base classes contain a function of the same name, can be solved by overriding the base class functions in the derived class. In this case, you can call the base class function explicitly in the overridden function of the derived class. Listing 23 shows how to override a base class function in a derived class (you can find the OverridenMemberFunction.cpp file on the CD in the Code\Chapter7 folder):

▶ Listing 23: Resolving Ambiguity by Overriding a Base Class Function in a Derived Class

```
```cpp
#include<iostream.h>

class Myclass1
{
public:
```
```