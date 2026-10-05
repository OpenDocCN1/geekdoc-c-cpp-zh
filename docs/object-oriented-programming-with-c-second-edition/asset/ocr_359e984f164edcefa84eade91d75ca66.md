# Virtual Functions and Dynamic Polymorphism 161

address of A::abc() address of A::def()

| 101 | 201 | VTBL of class A |

**Figure 6.1** Table addresses of virtual functions of the base class

Similarly, a table of addresses of virtual functions will be created for the derived class also. If the derived class does not redefine a center base class member, then the table will contain the address of the inherited base class virtual function itself. But if a base class virtual function is redefined in the derived class, this table will contain the address of the overriding function. Finally, if the derived class defines a new virtual function, then its address will also be contained in the table. Thus, if class B is derived from class A as illustrated in Listing 6.11, then the VTBL for class B will appear as in Figure 6.2.

+   **Listing 6.11** Overriding base class virtual functions and introducing new ones

```
/*Beginning of A.h*/
#include="A.h"
class B : public A {
public:
    void def();
    virtual void ghi(); //overriding the A::def() function
                       //introduces a new virtual
                       //function
}
/*End of B.h*/
```

address of B::abc() address of B::ghi()

| 101 | 301 | 401 |

address of B::def()

**Figure 6.2** Table of addresses of virtual functions of the derived class

Notice that the A::abc() is not overridden in the derived class, its address reappears in the VTBL of class B. On the other hand, since the A::def() function was overridden in the derived class, its address is replaced in the VTBL of class B—the address of B::ghi() function which is a newly introduced virtual function in class B.
Finally, every object of a class that has a virtual function contains a pointer to the VTBL of the corresponding class. This pointer is known as the virtual pointer or VPTR. For example, object of class A, apart from all other non-static data members, will also have a pointer to the VTBL of class A. This table is depicted in Figure 6.1. Similarly, object of class B, apart from all other non-static data members, will also have a pointer to the VTBL of class B. This table is depicted in Figure 6.2. Now, whenever a call is dispatched to a virtual through an object or a reference to an object, or by a pointer to an object, then