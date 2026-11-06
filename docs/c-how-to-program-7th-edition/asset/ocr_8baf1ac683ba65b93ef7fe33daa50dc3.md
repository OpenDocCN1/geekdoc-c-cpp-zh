object code for the direct and indirect base classes of any derived classes used by the program. Suppose a client wants to create an application that uses class BasePlusCommissionEmployee, which is a derived class of CommissionEmployee (we'll see an example of this in Section 12.4.4). When compiling the client application, the client's object code must be linked with the object code for classes BasePlusCommissionEmployee and CommissionEmployee, because BasePlusCommissionEmployee inherits member functions from its base class CommissionEmployee. The code is also linked with the object code for any C++ Standard Library classes used in class CommissionEmployee, class BasePlusCommissionEmployee or the client code. This provides the program with access to the implementations of all of the functionality that the program may use.

# ### 12.4.4 CommissionEmployee–BasePlusCommissionEmployee Inheritance Hierarchy Using protected Data

To enable class BasePlusCommissionEmployee to directly access CommissionEmployee data members firstName, lastName, socialSecurityNumber, grossSales and commissionRate, we can declare those members as protected in the base class. As we discussed in Section 12.3, a base class's protected members can be accessed by members and friends of the base class and by members and friends of any classes derived from that base class.

> > **Good Programming Practice 12.1**
> > *Declare public members first, protected members second and private members last.*

# #### Defining Base Class CommissionEmployee with protected Data

Class CommissionEmployee (Figs. 12.12-12.13) now declares data members firstName, lastName, socialSecurityNumber, grossSales and commissionRate as protected (Fig. 12.12, lines 32-37) rather than private. The member-function implementations in Fig. 12.13 are identical to those in Fig. 12.5.

```
```cpp
// Fig. 12.12: CommissionEmployee.h
// CommissionEmployee class definition with protected data.
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ standard string class
using namespace std;

class CommissionEmployee
{
public:
   CommissionEmployee( const string &, const string &, const string &,
       double = 0.0, double = 0.0 );

   void setFirstName( const string & ); // set first name
   string getFirstName() const; // return first name
```
```

**Fig. 12.12** | CommissionEmployee class definition that declares protected data to allow access by derived classes. (Part 1 of 2.)