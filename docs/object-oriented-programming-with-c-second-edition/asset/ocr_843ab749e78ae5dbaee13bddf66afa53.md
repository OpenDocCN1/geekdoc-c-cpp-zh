it is able to access the value contained in only the four bytes. Thus, 'APtr' cannot access
an an area in the memory that has not been allocated. Therefore, a pointer of the base class type
can safely point at an object of the derived class, as illustrated by Figure 5.3.

![](bbox=[0.358, 0.157, 0.725, 0.335])

**Figure 5.3** Base class pointer points at an object of the derived class

We will soon realize that making a base class pointer point at an object of the derived class
is a very common requirement in C++ programming.
Now, let us find out why derived class pointers cannot be made to point at objects of the
base class without explicit typecasting, and why, even that is a unsafe thing to do. Now,
 us compile the main() function of Listing 5.5 and see the result.

# **Listing 5.5** Derived class pointer pointing at a base class

```
/*Beginning of DerivedPtr01.cpp*/
#include "B.h" //from listing 5.03
void main()
{
    A A1;
    B * BPtr; //line 1 - ERROR. Cannot convert from B* to
               //A1'.
    BPtr->x=10; //line 2 - OK. Derived class pointer
                //access base class member.
    BPtr->y=20; //line 3 - OK. Derived class pointer
                //access derived class member.
}
/*End of DerivedPtr01.cpp*/
```

Line 1 of Listing 5.5 will not compile because line 3 will. A derived class pointer cannot
point at an object of the base class. Let us see why. 'BPtr' is of type 'B *'. It is supposed to
point at objects of the derived class B. Therefore, it can access 'y'. Also 'BPtr' is pointing at
the next four bytes. Only 'A1', which occupies four bytes only, is able to access the value contained in thennext four bytes. There is a member of 'y' in class B. Thus, 'BPtr' is able to accessnan area in the memory that has not been allocated. Therefore, a pointer of the derived class
type cannot safely point at an object of the base class, as shown in Figure 5.4.

Line 3 of Listing 5.5 would write 20 into the bytes whose addresses are from 205 to 208.
But this block has not been allocated for the object which the pointer points. But this line
will compile. The problem is actually in line 1.