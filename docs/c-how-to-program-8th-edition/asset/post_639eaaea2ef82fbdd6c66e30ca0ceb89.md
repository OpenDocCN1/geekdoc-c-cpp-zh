
```cpp
// Fig. 12.10: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class derived from class
// CommissionEmployee.
#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class
#include "CommissionEmployee.h" // CommissionEmployee class declaration
using namespace std;

class BasePlusCommissionEmployee : public CommissionEmployee
{
public:
   BasePlusCommissionEmployee( const string &, const string &,
      const string &, double = 0.0, double = 0.0, double = 0.0 );

   void setBaseSalary( double ); // set base salary
   double getBaseSalary() const; // return base salary

   double earnings() const; // calculate earnings
   void print() const; // print BasePlusCommissionEmployee object
private:
   double baseSalary; // base salary
}; // end class BasePlusCommissionEmployee

#endif
```

**Fig. 12.10** | BasePlusCommissionEmployee class definition indicating inheritance relationship with class CommissionEmployee.

```cpp
// Fig. 12.11: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iostream>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
   const string &first, const string &last, const string &ssn,
   double sales, double rate, double salary )
   // explicitly call base-class constructor
   : CommissionEmployee( first, last, ssn, sales, rate )
{
   setBaseSalary( salary ); // validate and store base salary
} // end BasePlusCommissionEmployee constructor

// set base salary
void BasePlusCommissionEmployee::setBaseSalary( double salary )
{
```

**Fig. 12.11** | BasePlusCommissionEmployee implementation file: private base-class data cannot be accessed from derived class. (Part 1 of 3.)

```
C:\chhpt8_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(46) :
    error C2248: 'CommissionEmployee::commissionRate':
    cannot access private member declared in class 'CommissionEmployee'
```

**Fig. 12.11** | *BasePlusCommissionEmployee implementation file: private base-class data cannot be accessed from derived class.* (Part 3 of 3.)

Figure 12.11 shows BasePlusCommissionEmployee’s member-function implementations. The constructor (lines 8–15) introduces **base-class initializer syntax** (line 12), which uses a member initializer to pass arguments to the base-class (CommissionEmployee) constructor. C++ requires that a derived-class constructor call its base-class constructor to initialize the base-class data members that are inherited into the derived class. Line 12 does this by *explicitly* invoking the CommissionEmployee constructor by name, passing the constructor’s parameters first, last, ssn, sales and rate as arguments to initialize the base-class data members firstName, lastName, socialSecurityNumber, grossSales and commissionRate. If BasePlusCommissionEmployee’s constructor did not invoke class CommissionEmployee’s constructor *explicitly*, C++ would attempt to invoke class CommissionEmployee’s default constructor implicitly—but the class does not have such a constructor, so the compiler would issue an error. Recall from Chapter 3 that the compiler provides a default constructor with no parameters in any class that does *not* explicitly include a constructor. However, CommissionEmployee *does* explicitly include a constructor, so a default constructor is *not* provided.

> **Common Programming Error 12.1**
>
> When a derived-class constructor calls a base-class constructor, the arguments passed to the base-class constructor must be consistent with the number and types of parameters specified in one of the base-class constructors; otherwise, a compilation error occurs.

![](img/bfd978e7e9b192bab46ec2a89e481263_550_0.png)

> **Performance Tip 12.1**
>
> In a derived-class constructor, invoking base-class constructors and initializing member object explicitly in the member initializer list prevents duplicate initialization in which a default constructor is called, then data members are modified again in the derived-class constructor’s body.

![](img/bfd978e7e9b192bab46ec2a89e481263_550_1.png)

## Compilation Errors from Accessing Base-Class private Members

The compiler generates errors for line 36 of Fig. 12.11 because base class CommissionEmployee’s data members commissionRate and grossSales are private—derived class BasePlusCommissionEmployee’s member functions are not allowed to access base class CommissionEmployee’s private data. The compiler issues additional errors in lines 43–46 of BasePlusCommissionEmployee’s print member function for the same reason. As you can see, C++ rigidly enforces restrictions on accessing private data members, so that even a *derived class (which is intimately related to its base class) cannot access the base class’s private data.*

## Preventing the Errors in BasePlusCommissionEmployee

We purposely included the erroneous code in Fig. 12.11 to emphasize that a derived class’s member functions cannot access its base class’s private data. The errors in BasePlusCommissionEmployee could have been prevented by using the *get* member functions inherited from class CommissionEmployee. For example, line 36 could have invoked getCommissionRate and getGrossSales to access CommissionEmployee’s private data members commissionRate and grossSales, respectively. Similarly, lines 43–46 could have used appropriate *get* member functions to retrieve the values of the base class’s data members. In the next example, we show how using protected data also allows us to avoid the errors encountered in this example.

### Including the Base-Class Header in the Derived-Class Header with #include

Notice that we #include the base class’s header in the derived class’s header (line 8 of Fig. 12.10). This is necessary for three reasons. First, for the derived class to use the base class’s name in line 11, we must tell the compiler that the base class exists—the class definition in CommissionEmployee.h does exactly that.

The second reason is that the compiler uses a class definition to determine the size of an object of that class (as we discussed in Section 3.6). A client program that creates an object of a class must #include the class definition to enable the compiler to reserve the proper amount of memory for the object. When using inheritance, a derived-class object’s size depends on the data members declared explicitly in its class definition and the data members inherited from its direct and indirect base classes. Including the base class’s definition in line 8 allows the compiler to determine the memory requirements for the base class’s data members that become part of a derived-class object and thus contribute to the total size of the derived-class object.

The last reason for line 8 is to allow the compiler to determine whether the derived class uses the base class’s inherited members properly. For example, in the program of Figs. 12.10–12.11, the compiler uses the base-class header to determine that the data members being accessed by the derived class are private in the base class. Since these are inaccessible to the derived class, the compiler generates errors. The compiler also uses the base class’s *function prototypes* to validate function calls made by the derived class to the inherited base-class functions.

### Linking Process in an Inheritance Hierarchy

In Section 3.7, we discussed the linking process for creating an executable GradeBook application. In that example, you saw that the client’s object code was linked with the object code for class GradeBook, as well as the object code for any C++ Standard Library classes used either in that example or in class GradeBook.

The linking process is similar for a program that uses classes in an inheritance hierarchy. The process requires the object code for all classes used in the program and the object code for the direct and indirect base classes of any derived classes used by the program. Suppose a client wants to create an application that uses class BasePlusCommissionEmployee, which is a derived class of CommissionEmployee (we’ll see an example of this in Section 12.4.4). When compiling the client application, the client’s object code must be linked with the object code for classes BasePlusCommissionEmployee and CommissionEmployee, because BasePlusCommissionEmployee inherits member functions from its base class CommissionEmployee. The code is also linked with the object code for any C++ Standard Library classes used in class CommissionEmployee, class BasePlusCommissionEmployee or the client code. This provides the program with access to the implementations of all of the functionality that the program may use.
