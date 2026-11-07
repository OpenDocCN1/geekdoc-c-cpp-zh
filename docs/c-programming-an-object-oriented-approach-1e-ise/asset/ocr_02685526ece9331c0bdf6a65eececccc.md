**Implementation** Program 13.17 shows the implementation for functions declared in the *Poly* class.

# **Program 13.17**  File poly.cpp

```
```cpp
/**************************************************************
 * The implementation file for the Poly class                  *
 **************************************************************/
#include "poly.h"

// Default constructor
Poly :: Poly ()
:degree (0)
{
    ptr = 0;
}
// Parameter constructor
Poly :: Poly (int deg)
:degree (deg)
{
    ptr = new double [degree + 1];
    for (int i = degree; i >= 0; i--)
    {
        ptr [i] = 0.0;
    }
}
// A constructor that creates an object of one term
Poly :: Poly (int deg, double coef)
:degree (deg)
{
    ptr = new double [degree + 1];
    for (int i = degree; i >= 0; i--)
    {
        ptr [i] = 0.0;
    }
    ptr [degree] = coef;
}
// Destructor
Poly :: ~Poly ()
{
    delete [ ] ptr;
}
// Copy constructor
Poly :: Poly (const Poly& origin)
{
    ptr = new double [degree + 1];
```
```