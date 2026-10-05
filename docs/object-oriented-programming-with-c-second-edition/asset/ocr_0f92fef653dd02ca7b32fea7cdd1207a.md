# Classes and Objects 47

he/she has not defined. Data abstraction is effective to data hiding (recall the case of the overhead projector systems discussed earlier).

On the other side of the coin, in C language, life becomes difficult for an application programmer. If a certain member of the structure acquires an invalid or a wrong value, he/she has to hunt through the entire source code to detect the bug. This problem rapidly gains significance as the code length increases. In actual practice, it is common to have code of more than 25,000 lines.

Let us now some as follows:
Perfect definitions of the member functions are guaranteed to achieve their objective because of data hiding.

This is the essence of the object-oriented programming system. Real-world objects have not only working parts but also an exclusive interface to these inner-working parts. A perfect interface is guaranteed to work because of its exclusive rights.

# 2.1.8 Explicit Address Manipulation

An application programmer can manipulate the member data of any object by explicit address manipulation. Listing 2.12 illustrates the point.

Listing 2.12 Explicit address manipulation

```
/*Beginning of AddrManip.cpp*/
#include<Distance.h>
#include<iostream.h>

void main()
{
    Distance d1;
    d1.setFeet(256);
    d1.setInches(2.2);
    char * p=(char *)&d1; //explicit address manipulation
    *p=1; //undesirable but unpreventable
    cout<<d1.getFeet()<<" "<<d1.getInches()<<endl;
}
/*End of AddrManip.cpp*/
```

Output
257 2.2

However, such explicit address manipulation by an application programmer cannot be prevented. It is left as an exercise for the readers to explain the output of the above paragraph (Listing 2.12).

# 2.1.9 Arrow Operator

Member functions can be called with respect to an object through a pointer pointing at the object. The arrow operator (->) does this. An illustrative example is shown in Listing 2.13.

Listing 2.13 Accessing members through pointers

```
/*Beginning of PointerMember.cpp*/
#include<iostream.h>
#include"Distance.h"
```