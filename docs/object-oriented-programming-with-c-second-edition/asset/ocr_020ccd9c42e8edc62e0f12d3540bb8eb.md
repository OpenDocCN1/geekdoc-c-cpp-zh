Smart pointers, unlike the ordinary smart pointers, can be designed to inevitably point at valid objects. In contrast, the ordinary smart pointers have to be explicitly initialized by the client. Consequently, they have to be tested for validity before every use. Smart pointers are class objects. Let us create a class objects will behave like pointers to the class String. See Listing 8.59.

# Listing 8.59 A class of smart pointers

```
/*Beginning of StrPtr.h*/
#include "String.h"
class StrPtr
{
    String * p;
public:
    StrPtr(String&); //the one and only constructor
};
/*End of StrPtr.h*/
/*Beginning of StrPtr.cpp*/
#include "String.h"
StrPtr::StrPtr(String& ss)
{
    p=ss;
}
/*End of StrPtr.cpp*/
```

We must notice how a zero-argument constructor has been deliberately left out from the the class definition in Listing 8.59. This forces clients to invariably pass an object of the class String as a parameter when they create objects of the class StrPtr. Therefore, the embedded pointer of the class StrPtr always points at an object of the class String. The client can create an object of the class in Listing 8.59 as follows:

StrPtr si("abc");
StrPtr p(si);

To mimic a pointer completely, the objects of the class StrPtr should be capable of being used as follows:

```
p->setString("def");
```

For this, the pointer-to-member operator (->) needs to be overloaded for the class StrPtr. This can be done as in Listing 8.60.

# Listing 8.60 Overloading the pointer-to-member operator for smart pointers

```
/*Beginning of StrPtr.h*/
#include "String.h"
class StrPtr
{
    String * p;
public:
    StrPtr(String&);
    String * operator->(); //the one and only constructor
};
/*End of StrPtr.h*/
/*Beginning of StrPtr.cpp*/
#include "String.h"
```