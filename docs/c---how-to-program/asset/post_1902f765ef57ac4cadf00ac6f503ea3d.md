
objects' names to invoke their member functions. We now examine the relationships among classes in a hierarchy more closely. The next several sections present a series of examples that demonstrate how base-class and derived-class pointers can be aimed at base-class and derived-class objects, and how those pointers can be used to invoke member functions that manipulate those objects.

- In Section 20.3.1, we assign the address of a derived-class object to a base-class pointer, then show that invoking a function via the base-class pointer invokes the base-class functionality in the derived-class object—i.e., the type of the handle determines which function is called.
- In Section 20.3.2, we assign the address of a base-class object to a derived-class pointer, which results in a compilation error. We discuss the error message and investigate why the compiler does not allow such an assignment.
- In Section 20.3.3, we assign the address of a derived-class object to a base-class pointer, then examine how the base-class pointer can be used to invoke only the base-class functionality—when we attempt to invoke derived-class member functions through the base-class pointer, compilation errors occur.
- Finally, in Section 20.3.4, we demonstrate how to get polymorphic behavior from base-class pointers aimed at derived-class objects. We introduce virtual functions and polymorphism by declaring a base-class function as virtual. We then assign the address of a derived-class object to the base-class pointer and use that pointer to invoke derived-class functionality—precisely the capability we need to achieve polymorphic behavior.

A key concept in these examples is to demonstrate that with public inheritance an object of a derived class can be treated as an object of its base class. This enables various interesting manipulations. For example, a program can create an array of base-class pointers that point to objects of many derived-class types. Despite the fact that the derived-class objects are of different types, the compiler allows this because each derived-class object is an object of its base class. However, we cannot treat a base-class object as an object of any of its derived classes. For example, a CommissionEmployee is not a BasePlusCommissionEmployee in the hierarchy defined in Chapter 19—a CommissionEmployee does not have a baseSalary data member and does not have member functions setBaseSalary and getBaseSalary. The is-a relationship applies only from a derived class to its direct and indirect base classes.

## 20.3.1 Invoking Base-Class Functions from Derived-Class Objects

The example in Fig. 20.1 reuses the final versions of classes CommissionEmployee and BasePlusCommissionEmployee from Section 19.3.5. The example demonstrates three ways to aim base- and derived-class pointers at base- and derived-class objects. The first two are natural and straightforward—we aim a base-class pointer at a base-class object and invoke base-class functionality, and we aim a derived-class pointer at a derived-class object and invoke derived-class functionality. Then, we demonstrate the relationship between derived classes and base classes (i.e., the is-a relationship of inheritance) by aiming a base-class pointer at a derived-class object and showing that the base-class functionality is indeed available in the derived-class object.

```cpp
// Fig. 20.1: fig20_01.cpp
// Aiming base-class and derived-class pointers at base-class
// and derived-class objects, respectively.
#include <iostream>
#include <iomanip>
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;

int main()
{
    // create base-class object
    CommissionEmployee commissionEmployee(
        "Sue", "Jones", "222-22-2222", 10000, .06 );

    // create base-class pointer
    CommissionEmployee *commissionEmployeePtr = nullptr;

    // create derived-class object
    BasePlusCommissionEmployee basePlusCommissionEmployee(
        "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );

    // create derived-class pointer
    BasePlusCommissionEmployee *basePlusCommissionEmployeePtr = nullptr;

    // set floating-point output formatting
    cout << fixed << setprecision( 2 );

    // output objects commissionEmployee and basePlusCommissionEmployee
    cout << "Print base-class and derived-class objects:\n\n";
    commissionEmployee.print(); // invokes base-class print
    cout << "\n\n";
    basePlusCommissionEmployee.print(); // invokes derived-class print

    // aim base-class pointer at base-class object and print
    commissionEmployeePtr = &commissionEmployee; // perfectly natural
    cout << "\n\nCalling print with base-class pointer to "
         << "base-class object invokes base-class print function:\n\n";
    commissionEmployeePtr->print(); // invokes base-class print

    // aim derived-class pointer at derived-class object and print
    basePlusCommissionEmployeePtr = &basePlusCommissionEmployee; // natural
    cout << "\n\nCalling print with derived-class pointer to "
         << "derived-class object invokes derived-class "
         << "print function:\n";
    basePlusCommissionEmployeePtr->print(); // invokes derived-class print

    // aim base-class pointer at derived-class object and print
    commissionEmployeePtr = &basePlusCommissionEmployee;
    cout << "\n\nCalling print with base-class pointer to "
         << "derived-class object\ninvokes base-class print "
         << "function on that derived-class object:\n\n";
    commissionEmployeePtr->print(); // invokes base-class print
    cout << endl;
} // end main
```

Fig. 20.1 | Assigning addresses of base-class and derived-class objects to base-class and derived-class pointers. (Part 1 of 2.)

Fig. 20.1 | Assigning addresses of base-class and derived-class objects to base-class and derived-class pointers. (Part 2 of 2.)

Print base-class and derived-class objects:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Calling print with base-class pointer to
base-class object invokes base-class print function:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

Calling print with derived-class pointer to derived-class object invokes derived-class print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Calling print with base-class pointer to derived-class object
invokes base-class print function on that derived-class object:

commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04 ² Notice that the base salary is not displayed

Recall that each BasePlusCommissionEmployee object is a CommissionEmployee that *also* has a base salary. Class BasePlusCommissionEmployee’s earnings member function (lines 34–37 of Fig. 19.15) redefines the CommissionEmployee’s earnings member function (lines 85–88 of Fig. 19.14) to include the object’s base salary. Class BasePlusCommissionEmployee’s print member function (lines 40–48 of Fig. 19.15) redefines class CommissionEmployee’s version (lines 91–98 of Fig. 19.14) to display the same information *plus* the employee’s base salary.

CommissionEmployee object does not provide a setBaseSalary member function, nor does it provide a baseSalary data member to set. This could lead to problems, because member function setBaseSalary would assume that there is a baseSalary data member to set at its “usual location” in a BasePlusCommissionEmployee object. This memory does not belong to the CommissionEmployee object, so member function setBaseSalary might overwrite other important data in memory, possibly data that belongs to a different object.

```cpp
// Fig. 20.2: fig20_02.cpp
// Aiming a derived-class pointer at a base-class object.
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"

int main()
{
  CommissionEmployee commissionEmployee(
    "Sue", "Jones", "222-22-2222", 10000, .06);
  BasePlusCommissionEmployee *basePlusCommissionEmployeePtr = nullptr;

  // aim derived-class pointer at base-class object
  // Error: a CommissionEmployee is not a BasePlusCommissionEmployee
  basePlusCommissionEmployeePtr = &commissionEmployee;
} // end main
```

Microsoft Visual C++ compiler error message:

> C:\examples\ch20\Fig20_02\fig20_02.cpp(14): error C2440: '=' : cannot convert from 'CommissionEmployee *' to 'BasePlusCommissionEmployee *'
> Cast from base to derived requires dynamic_cast or static_cast

Fig. 20.2 | Aiming a derived-class pointer at a base-class object.

## 20.3.3 Derived-Class Member-Function Calls via Base-Class Pointers

Off a base-class pointer, the compiler allows us to invoke only base-class member functions. Thus, if a base-class pointer is aimed at a derived-class object, and an attempt is made to access a derived-class-only member function, a compilation error will occur.

Figure 20.3 shows the consequences of attempting to invoke a derived-class member function off a base-class pointer. [Note: We're again reusing the versions of classes CommissionEmployee and BasePlusCommissionEmployee from Section 19.3.5.] Line 11 creates commissionEmployeePtr—a pointer to a CommissionEmployee object—and lines 12–13 create a BasePlusCommissionEmployee object. Line 16 aims the base-class commissionEmployeePtr at derived-class object basePlusCommissionEmployee. Recall from Section 20.3.1 that this is allowed, because a BasePlusCommissionEmployee is a CommissionEmployee (in the sense that a BasePlusCommissionEmployee object contains all the functionality of a CommissionEmployee object). Lines 20–24 invoke base-class member functions getFirstName, getLastName, getSocialSecurityNumber, getGrossSales and getCommissionRate off the base-class pointer. All of these calls are allowed, because BasePlusCommissionEmployee inherits these member functions from CommissionEmployee. We know that commissionEmployeePtr is aimed at a BasePlusCommissionEmployee object, so in lines 28–29 we attempt to invoke BasePlusCommissionEmployee member
