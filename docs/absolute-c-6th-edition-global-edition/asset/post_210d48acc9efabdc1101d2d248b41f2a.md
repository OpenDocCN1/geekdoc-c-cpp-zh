
# Display 15.2　Implementation of the Base Class Sale (part 1 of 2)

```cpp
//This is the file sale.cpp.
//This is the implementation for the class Sale.
//The interface for the class Sale is in the file sale.h.

#include <iostream>
#include "sale.h"
using std::cout;

namespace SavitchSale
{
    Sale::Sale( ) : price(0)
    {
        //Intentionally empty
    }

    Sale::Sale(double thePrice)
    {
        if (thePrice >= 0)
            price = thePrice;
        else
        {
            cout << "Error: Cannot have a negative price!\n";
            exit(1);
        }
    }

    double Sale::bill( ) const
    {
        return price;
    }

    double Sale::getPrice( ) const
    {
        return price;
    }

    void Sale::setPrice(double newPrice)
    {
        if (newPrice >= 0)
            price = newPrice;
        else
        {
            cout << "Error: Cannot have a negative price!\n";
            exit(1);
        }
    }

    double Sale::savings(const Sale& other) const
    {
        return (bill( ) - other.bill( ));
    }
```
```

# Display 15.2 Implementation of the Base Class Sale (part 2 of 2)

```
46    bool operator < (const Sale& first, const Sale& second)
47    {
48        return {first.bill() < second.bill()};
49    }
50 }//SavitchSale
```

define derived classes of the class Sale and define their versions of the member function bill; the definitions of the member function savings and the overloaded operator, <, which we gave with the class Sale, will use the version of the member function bill that corresponds to the object of the derived class.

For example, Displays 15.3 and 15.4 show the derived class DiscountSale. Notice that the class DiscountSale requires a different definition for its version of the member function bill. Nonetheless, when the member function savings and the overloaded operator, <, are used with an object of the class DiscountSale, they will use the version of the function definition for bill that was given with the class DiscountSale. This is indeed a pretty fancy trick for C++ to pull off. Consider the function call d1.savings(d2) for objects d1 and d2 of the class DiscountSale. The definition of the function savings (even for an object of the class DiscountSale) is given in the implementation file for the base class Sale, which was compiled before we even thought of the class DiscountSale. Yet, in the function call d1.savings(d2), the line that calls the function bill knows enough to use the definition of the function bill given for the class DiscountSale.

How does this work? In order to write C++ programs you can just assume it happens by magic, but the real explanation was given in the introduction to this section. When you label a function virtual, you are telling the C++ environment "Wait until this function is used in a program, and then get the implementation corresponding to the calling object."

Display 15.5 gives a sample program that illustrates how the virtual function bill and the functions that use bill work in a complete program.

# Display 15.3 Interface for the Derived Class DiscountSale (part 1 of 2)

```
//This is the file discountsale.h
//This is the interface for the class DiscountSale.

#ifndef DISCOUNTSALE_H
#define DISCOUNTSALE_H
#include "sale.h"

namespace SavitchSale
{

class DiscountSale : public Sale
{
public:
    DiscountSale();
    DiscountSale(double thePrice, double theDiscount);
    //Discount is expressed as a percentage of the price.
    //A negative discount is a price increase.
```

# Display 15.3　Interface for the Derived Class `DiscountSale` (part 2 of 2)

```
```cpp
15    double getDiscount() const;
16    void setDiscount(double newDiscount);
17    double bill() const;
18  private:
19    double discount;
20  };
21  }//SavitchSale
22 #endif//DISCOUNTSALE_H
```
```

**Note:** Since `bill` was declared virtual in the base class, it is automatically virtual in the derived class `DiscountSale`. You can add the modifier `virtual` to the declaration of `bill` in `DiscountSale`, as here; either case `bill` is virtual in the class `DiscountSale`. (We prefer to include the word `virtual` in all virtual function declarations, even if it is not required. We omitted it here to illustrate that it is not required.)

# Display 15.4　Implementation for the Derived Class `DiscountSale` (part 1 of 2)

```
```cpp
1  //This is the implementation for the class DiscountSale.
2  //This is the file discountsale.cpp.
3  //The interface for the class DiscountSale is in the header file
4  //discountsale.h.
5  #include "discountsale.h"
6
7  namespace SavitchSale
8  {
9      DiscountSale::DiscountSale( ) : Sale( ), discount(0)
10     {
11         //Intentionally empty
12     }
13
14     DiscountSale::DiscountSale(double thePrice, double theDiscount)
15         : Sale(thePrice), discount(theDiscount)
16     {
17         //Intentionally empty
18     }
19
20     double DiscountSale::getDiscount( ) const
21     {
22         return discount;
23     }
24
25     void DiscountSale::setDiscount(double newDiscount)
26     {
27         discount = newDiscount;
28     }
29
30     double DiscountSale::bill( ) const
31     {
32         double fraction = discount / 100;
33         return (1 - fraction) * getPrice( );
34     }
35  }//SavitchSale
```
```

You do not repeat the qualifier `virtual` in the function definition.

# Display 15.5 Use of a Virtual Function

```
//Demonstrates the performance of the virtual function bill.
#include <iostream>
#include "sale.h"//Not really needed, but safe due to ifndef.
#include "discountsale.h"
using std::cout;
using std::endl;
using std::ios;
using namespace SavitchSale;

int main()
{
    Sale simple(10.00);//One item at $10.00.
    DiscountSale discount(11.00, 10);
    //One item at $11.00 with a 10% discount

    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);

    if (discount < simple)
    {
        cout << "Discounted item is cheaper.\n";
        cout << "Savings is $" << simple.savings(discount) << endl;
    }
    else
        cout << "Discounted item is not cheaper.\n";

    return 0;
}
```

The objects discount and simple use different code for the member function bill when the less-than comparison is made. Similar remarks apply to savings.

# Sample Dialogue

```
Discounted item is cheaper.
Savings is $0.10
```

# Virtual Function

A virtual function is indicated by including the modifier virtual in the member function declaration (which is given in the definition of the class).

If a function is virtual and a new definition of the function is given in a derived class, then for any object of the derived class, that object will always use the definition of the virtual function that was given in the derived class, even if the virtual function is used indirectly by being invoked in the definition of an inherited function. This method of deciding which definition of a virtual function to use is known as late binding.

# Polymorphism

Polymorphism refers to the ability to associate many meanings to one function name by means of the late-binding mechanism. Thus, polymorphism, late binding, and virtual functions are really all the same topic.

# Overriding

When a virtual function definition is changed in a derived class, programmers often say the function definition is overridden. In the C++ literature, a distinction is usually made between the terms redefined and overridden. Both terms refer to changing the definition of the function in a derived class. If the function is a virtual function, this act is called overriding. If the function is not a virtual function, it is called redefining. This may seem like a silly distinction to you the programmer, since you do the same thing in both cases, but the two cases are treated differently by the compiler.

# Provide Context with C++11's override Keyword

When we override a virtual function, sometimes it is not clear whether the programmer meant to override the function. Additionally, if we are only looking at the derived class, it may not be clear which functions are being overridden in the base class. These problems can be addressed in C++11 by using the new override keyword. For example, in Displays 15.1 to 15.4 the virtual function bill() is overridden in the DiscountSale class:

```
class Sale
{
public:
...
virtual double bill() const;
...
};

class DiscountSale : public Sale
{
public:
...
double bill() const;
...
};
```

If we are only looking at the DiscountSale class, it is not clear that bill() is overriding a function in the Sale class. It is also possible (though unlikely) that the programmer made an error and didn't intend to make bill() a virtual function in the Sale class.
