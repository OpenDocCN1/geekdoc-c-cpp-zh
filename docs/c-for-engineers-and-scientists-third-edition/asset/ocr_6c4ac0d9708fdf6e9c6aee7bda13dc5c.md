# Chapter 11 Polymorphism 655

The following output is produced by Program 11.15:

The computed value using a base class object call is 36
The computed value using a derived class object call is 36

As this shows, the same result is obtained, no matter what object type calls the f2() function, because the derived class doesn't have an override of the base class f2() function. Therefore, both calls to f2() in the base class f2() are being called.
After the base class f2() is called, it always calls the base class of f1() rather than the derived class version. This behavior is caused by a process referred to function binding. In normal function, static binding is used, makes the determination of which function is called at compile time. Therefore, when the compiler first encounters f1() in the base, it makes the determination that whenever f2() is called from either a base or derived class, it subsequently calls the base class f1() function.
In place of static binding, you would like a binding method of determining which function should be called at runtime, based on the object type making the call. This type of binding, referred to as dynamic binding, is achieved in C++ with virtual functions. The virtual function compiles to create a pointer to, but not in the pointer's value until the function is actually called. Then at runtime, based on the object making the call, this is identical to Program 11.15, except for the virtual declaration of the f1() function.
Creating a virtual function is easy—simply place the keyword virtual before the function's return type in the declaration section. For example, Program 11.16, which is identical to Program 11.15, except for the virtual declaration of the f1() function.

![](bbox=[0.113, 0.503, 0.183, 0.563])

# Program 11.16

```
#include <iostream>
#include <cmath>
using namespace std;

// class declaration section for the base class
class One {
protected:
    double a;
public:
    One(double = 2.0); // constructor
    virtual double f1(double); // a member function
    double f2(double); // another member function
};
```

![](bbox=[0.843, 0.836, 0.883, 0.856])