# 222 Object-Oriented Programming with C++

# Listing 8.12 Declaring member function to overload the increment operator

```
/*Beginning of Distance.h*/
class Distance
{
    public:
    /*
    rest of the class Distance
    */
    Distance operator ++ ();
};
/*End of Distance.h*/
/*Beginning of Distance.cpp*/
#include "Distance.h"
Distance Distance :: operator ++ ()
{
    return Distance(+iFeet, fInches);
}
/*ndefinitions of the rest of the functions of class
Distance
*/
/*End of Distance.cpp*/
```

The operator-overloading function should be public because it will mostly be called from functions that are not members of the class Distance. It should not be a constant member function because it would verily modify the value of at least one of the data members (iFeet) of the calling object. Although the definition of the operator-overloading function appears cryptic, it is in fact very simple (and economical). First, the increment operator works (it is in prefix notation). Thus, the iFeet data member of the calling object gets incremented. Second, the explicit call to the constructor creates a nameless object of the class Distance by passing the incremented value of iFeet and the unaltered value of fInches as parameters. Third, the operator-overloading function returns the nameless object constructed. If the call to the operator-overloading function is on the right-hand side of the assignment operator, the value of the returned object will expectedly be copied to the object on the left. Thus, our purpose is served.

However, we would like a different effect to be produced if we write the statement

```
d2 = d++;
```

In this case, we would like the initial value of 'd1' to get copied to 'd2', and, thereafter, the value of iFeet data member of 'd1' to get incremented. However, if the compiler interprets both the statements

```
d2 = ++d1;
```

and

```
d2 = d1++;
```

in identical ways, then we will have no way of writing the two different functions. Fortunately, this is not so. While the compiler interprets the statement

```
d2 = ++d1;
```

as

```
d2 = d1.operator ++ ();
```