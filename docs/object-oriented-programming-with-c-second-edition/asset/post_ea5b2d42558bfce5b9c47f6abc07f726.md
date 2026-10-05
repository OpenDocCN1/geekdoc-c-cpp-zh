
![](img/5bfa77b13fdaa376725789bb8c00ee79_138_0.png)

Figure 5.4 Derived class pointer pointing at an object of the base class

However, a derived class pointer can be forcibly to point at an object of the derived class by explicit typecasting, as illustrated by Listing 5.6. Continuing with classes A and B given in Listing 5.3.

+ Listing 5.6 Forcible typecasting to make a derived class pointer point at an object of the base class

```cpp
/*Beginning of DerivedPtrTypecast.cpp*/
#include"B.h"
//from listing 5.03
{
    A A1;
    B * BPtr;
    BPtr=(B*)&A1; //derived class pointer
                 //forcible typecasting to make derived
                 //class pointer point at base class
                 //object
}
/*End of DerivedPtrTypecast.cpp*/
```

But explicit address manipulation like this is obviously dangerous. Now, let us consider the realistic cases where the classes have private data members and public member functions (see Listing 5.7). The same explanations that have been given above will hold true even if the classes A and B have 'x' and 'y' as private data members, respectively.

+ Listing 5.7 Classes of Listing 5.3 with member functions

```cpp
/*Beginning of A.h*/
{
    int x;
    public:
        void setx(const int x);
        /*
            rest of the class A
        */
};
/*End of A.h*/
/*Beginning of B.h*/
#include"A.h"
class B : public A
{
```

# Object-Oriented Programming with C++

```cpp
int y;
public:
void sety(const int y=0);
/*
rest of the class B
*/
};
/*End of B.h*/
```

The member functions in Listing 5.5 access private data members of their respective classes.

# Listing 5.8 Base class pointer pointing at an object of the derived class

```cpp
/*Beginning of BasePtr02.cpp*/
#include "B.h"
void main()
{
  A * APtr;
B * BPtr;
APtr=(B*)&B1;
//OK: base class pointer points at
//derived class's object
APtr->sety(10);
//OK: accessing base class member
//through base class pointer
APtr->sety(20);
//ERROR: sety() is not a member of class A
}
/*End of BasePtr02.cpp*/
```

# Listing 5.9 Derived class pointer pointing at an object of the base class

```cpp
/*Beginning of DerivedPtr02.cpp*/
#include "B.h"
void main()
{
  A A1;
B * BPtr;
BPtr=(B*)&A1;
//ERROR: cannot convert A* to B
BPtr->sety(10);
//OK: Derived class pointer accesses
//base class member.
BPtr->sety(20);
//OK: Derived class pointer accesses
//derived class member.
}
/*End of DerivedPtr02.cpp*/
```

The fact that a base class pointer can point at an object of the derived class (see Listings 5.8 and 5.9) will not be surprising. After all, this is exactly what happens when we call a base class function with respect to an object of the derived class.

B1.sety(10);

Based on the knowledge we have gained about this pointer in Chapter 2, we know that the compiler will internally convert the statement to
setx(&B1);

The address of ‘B1’ (a derived class object) is passed as a parameter to the function.
The corresponding argument in the A::setx() function is this pointer of type `A * const` (Listing 5.10).

## 5.3 Function Overriding

Member functions of the base class can be overridden in the derived class. Defining a member function in the derived class in such a manner that its name and signature match those of a base class function is known as function overriding. Function overriding results in two functions of the same name and same signature. One of them is in the base class. The other one is in the derived class. An illustrative example follows in Listing 5.11.

Listing 5.10 This pointer in a base class member function points at the derived class invoking object

```cpp
void setx(A * const this, const int p)
{
    this->x=p;
}
```

Obviously, the this pointer points to ‘B1’, which is an object of the derived class.

Listing 5.11 Function overriding

```cpp
/*Beginning of A.h*/
class A {
public:
    void show()
{
        cout<<"show() function of class A called\n";
    }
};/*End of A.h*/
/*Beginning of B.h*/
#include"A.h"
class B : public A {
public:
    void show() //overriding A::show()
    {
        cout<<"show() function of class B called\n";
    }
};/*End of B.h*/
```

The show() function of class B has overridden the show() function of class A. Consequently, if the show() function is called with respect to an object of the derived class B, the show() function of class B will be called instead of the show() function of class A. See Listing 5.12.

Listing 5.12 Calling the overriding function

```cpp
/*Beginning of Override01.cpp*/
#include"B.h"
void main() {
    B B1;
    B1.show(); //B::show() called
```

}
/*End of Override01.cpp*/
```

Output
show() function of class B called

Whenever a function is called with respect to an object of a class, the compiler first searches for the function prototype in the same class. Only if this search fails, the compiler goes up the class hierarchy to look for the function prototype. In Listings 5.11 and 5.12, the show() function of class A was virtually hidden by the show() function of class B.

Of course, the overridden function of the base class will be called if it is called with respect to an object of the base class (Listing 5.13).

Listing 5.13 Calling the overridden function with respect to the base class

```cpp
/*Beginning of Override02.cpp*/
#include"B.h"
void main()
{
    A A1;
    A1.show(); //A::show() called
}
/*End of Override02.cpp*/
```

Output
show() function of class A

The overridden base function can still be called with respect to an object of the derived class by the scope resolution operator as illustrated in Listing 5.14.

Listing 5.14 Calling the overridden function forcibly with respect to the derived class

```cpp
/*Beginning of Override03.cpp*/
#include"B.h"
void main()
{
    B B1;
    B1::show(); //A::show()
}
/*End of Override03.cpp*/
```

show() function of class A

Function overriding is actually a form of function overloading. Our knowledge of this pointer makes this clear. The signatures of the overriding function and the overridden function are only apparently the same. They are actually different from each other. The actual prototype of the A::show() function is

```cpp
void show(A * const);
```

On the other hand, the actual prototype of the B::show() function is

```cpp
void show(B * const);
```

The overridden B::function can be called from the overriding function as follows.

```cpp
void B::show()
{
    A::show();
    /*
    rest of the B::show()
    */
}
```

The scope resolution operator is necessary to avoid infinite recursion. But, what is the use of function overriding? Function overriding appears to be nothing more than a fancy language construct. Function overriding becomes significant only when the base class function being overridden is virtual. More about virtual functions and how they implement dynamic polymorphism is illustrated in Chapter 6.

## 5.4 Base Class Initialization

A derived object is composed of data members of the derived class as well as those of the base class. We need to initialize all of these members while creating an object of the derived class. We must remember that when an object of the derived class is created, the compiler implicitly and inevitably binds a call to the base class constructor and then the derived class constructor with respect to the object.

Suppose A is the base class and B is its derived class. The statement

```cpp
B B1;

B B1(); //memory allocated for the object
B1.A();//base class constructor called
B1.B();//derived class constructor called
```

is converted into

Destructors are called in the reverse order. As we already know, explicitly calling the constructors and destructors, with respect to an existing object, is prohibited. Now, we look at Listing 5.15.

> Listing 5.15 Unsuccessful initialization of base class members

```cpp
/*Beginning of A.h*/
class A
{
public:
    A(const int=0);
    void setx(const int x=0);
    int getx(const);
};
/*End of A.h*/

/*Beginning of A.cpp*/
#include "A.h"

A::A(const int p)
{
    x=p;
}
```
