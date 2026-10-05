# 278 Object-Oriented Programming with C++

It returns the type of the passed value as a reference to an object of class type_info. The class type_info is defined in the header file typeinfo.h.

Two objects of the class type_info can be compared by using the 'equality' operator. The name of the type value passed to the typeid operator can also be determined using the type_info::name() function.

Values of fundamental data types, pointers to values of fundamental data types, and references to fundamental data types can be passed to the typeid operator. Listing 8.72.

# Listing 8.72 The typeid.cpp operator

```
/*Beginning of typeid.cpp*/
#include<typeinfo.h>
void main()
{
    char c;
    int i;
    float f;
    double d;

    cout<<typeid(c).name()<<endl;
    cout<<typeid(i).name()<<endl;
    cout<<typeid(f).name()<<endl;
    cout<<typeid(d).name()<<endl;

    if(typeid(i)==typeid(1.1)) //comparing int with float
        cout<<"i is not of the same type as 1.1";
    else
        cout<<"i is not of the same type as 1.1";
}
/*End of typeid.cpp*/
```

Output
char
int
float
double
i is not of the same type as L.1

Class objects, pointers to class objects, or references to class objects can also be passed to the typeid operator. However, for the typeid operator to work correctly, the class whose object, pointer, or reference is passed to it should be polymorphic in nature. Otherwise, either of the following will happen depending upon the compiler and in its settings:

+   The compiler would issue a compile-time warning about the statement in which the typeid operator has been called. The OS would throw a run-time error.

+   If a dereferenced base class pointer that points at a derived class object is as a parameter to the typeid operator, the typeid operator would not be able to determine the type of the object pointed at by the pointer. It would instead return the base class type as the type of the object pointed at by the base class pointer, which of course is undesirable.