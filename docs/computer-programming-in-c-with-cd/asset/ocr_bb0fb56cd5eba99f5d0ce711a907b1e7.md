```
```cpp
class C:public B,public A
{
...
};
```
```

This changed order of inheritance also affects the order of constructor invocation and of destructor invocation for all the three classes: A, B, and C. Now, the object of class C, within the main() function, invokes the constructor of class B first, then it invokes the constructor of class A, and then the constructor of the class C. However, the destructors are invoked in the opposite sequence, that is, the destructor of the class C is invoked first, then the destructor of class A is invoked, and finally, the destructor of class B.

What happens when the base classes in multiple inheritance have constructors with parameters? In such a case, the derived class invokes the base class constructors explicitly. Listing 21 shows explicit invocation of base class constructors in multiple inheritance (you can find the ExplicitInvokeBaseCons.cpp file on the CD in the Code\Chapter7 folder).

# ▶ Listing 21: Invoking a Base Class Constructor Explicitly in Multiple Inheritance

```
```cpp
#include<iostream.h>

class A
{
    public:
    A()
    {
        cout<<"Default Constructor of A class"<<endl;
    }
    A(int a)
    {
        cout<<"Parameterized constructor of A class, storing the value of
        a="<<a<<endl;
    }
};
class B
{
    public:
    B()
    {
        cout<<"Default Constructor of B class"<<endl;
    }
};
class C:public A, public B
{
    public:
    C()
    {
        cout<<"Default Constructor of B class"<<endl;
```
```