# DISPLAY 15.11 The Derived Class DiscountSale (part 2 of 2)

```
//This is the implementation for the class DiscountSale.
#include "discountsale.h"  This is the file discountsale.cpp.

namespace salesavitch
{
    DiscountSale::DiscountSale() : Sale(), discount(0)
    {}
    DiscountSale::DiscountSale(double thePrice, double theDiscount)
        : Sale (thePrice), discount(theDiscount)
    {}
    double DiscountSale::bill ( ) const
    {
        double fraction = discount/100;
        return (1 - fraction)*price;
    }
}//salesavitch
```

DiscountSale. This is indeed a pretty fancy trick for C++ to pull off. Consider the function call d1.savings(d2) for objects d1 and d2 of the class DiscountSale. The definition of the function savings (even for an object of the class DiscountSale) is given in the implementation file for the base class Sale, which was compiled before we ever even thought of the class DiscountSale. Yet, in the function call d1.savings(d2), the line that calls the function bill knows enough to use the definition of the function bill given for the class DiscountSale.

How does this work? In order to write C++ programs, you can just assume it happens by magic, but the real explanation was given in the introduction to this section. When you label a function virtual, you are telling the C++ environment, “Wait until this function is used in a program, and then get the implementation corresponding to the calling object.”

Display 15.12 gives a sample program that illustrates how the virtual function bill and the functions that use bill work in a complete program.

# DISPLAY 15.12 Use of a Virtual Function (part 1 of 2)

```
//Demonstrates the performance of the virtual function bill.
#include <iostream>
#include "sale.h" //Not really needed, but safe due to ifndef.
#include "discountsale.h"
using namespace std;
using namespace salesavitch;
```