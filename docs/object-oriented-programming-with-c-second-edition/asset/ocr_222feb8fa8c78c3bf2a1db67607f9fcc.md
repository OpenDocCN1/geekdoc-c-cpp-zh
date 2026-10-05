Inheritance 123

Note: There are exceptions to the above assertion. The compiler will prevent a base class pointer from pointing at an object of the derived under certain circumstances. These are described later in this chapter.

First, let us understand why no harm can come by making a base class pointer point at an object of the derived. To understand this, we consider the classes of Listing 5.3.

# Listing 5.3 A derived class and its base class

```
/*Beginning of A.h*/
class A
{
    public:
    int x;
};
/*End of A.h*/
```

```
/*Beginning of B.h*/
#include "A.h"
class B : public A //derived from A
{
    public:
    int y;
};
/*End of B.h*/
```

These classes have only data members. There are no member functions and even these member data are public. These classes are given here to initially understand the concepts only. Explanations with classes that have private data members and public member functions are given later.

Now, let compile the main() function of Listing 5.4 and see what happens.

# Listing 5.4 Base class pointer pointing at a derived class object

```
/*Beginning of BasePtr0.cpp*/
#include "B.h" //from listing 5.0
void main()
{
    A * APtr;
    B B1;
    APtr=\&B1; //line 1 OK: base class pointer points at
               //derived class's object
    APtr->x=20; //line 2 OK: accessing base class member
               //through base class pointer
    APtr->y= //line 3 ERROR: y not found in class A
}
/*End of BasePtr0.cpp*/
```

Line 1 of Listing 5.4 will compile because line 3 will not. A base class pointer can point at an object of the derived class. Let us see why. 'APtr' is of type 'A *'. It is supposed to point at objects of the base class A. Therefore, it cannot access 'y'. 'y' in class A. The fact that 'APtr' points at an object of the derived class is of no significance. Through 'APtr', it is possible to access 'x' because there is a member named 'x' in class A. Although 'APtr' points at 'B1', which occupies eight bytes (four for 'x' and four for 'y'),