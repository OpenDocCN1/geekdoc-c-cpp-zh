# Object-Oriented Programming with C++

After

```
class A
{

    public:
    A();      //prototype inserted implicitly by compiler
    ...
    ...
};
```

```
A::A()
{
    //empty definition inserted implicitly by compiler
}
```

As we can see, the name of the constructor is the same as the name of the class. Also, the constructor does not return anything. The compiler defines the constructor in order to resolve the call to the constructor that it compulsory places for the object being created.

For reasons we will discuss later, it is forbidden to call the constructor explicitly for an existing object as follows.

```
A::A(); //not legal C++ code
```

# 4.1.1 Zero-argument Constructor

We can define and outline our constructors if the need arises. If we do so, the compiler does not define the constructor. However, it still embeds calls to the constructor as before.

The constructor is a non-static member function. It is called for an object, therefore, takes the this pointer as a formal argument just like other non-static member functions. Correspondingly, the address of the invoking object is passed as a parameter to the constructor call. This means that the members of the invoking object can be accessed from within the definition of the constructor.

Let us add our constructor to class A defined in Listing 4.1 and verify whether the constructor is actually implicitly by the compiler or not. See Listing 4.2.

> Listing 4.2 Constructors called for each object when the object is created

```
/*Beginning of A.h*/nclass A
{
    int x;
    public:
    A();
    void setx(const int=0); //our own constructor
    int getx();
};
/*End of A.h*/
```

```
/*Beginning of A.cpp*/
#include<A.h"
#include<iostream.h>
A::A() //our own constructor
```