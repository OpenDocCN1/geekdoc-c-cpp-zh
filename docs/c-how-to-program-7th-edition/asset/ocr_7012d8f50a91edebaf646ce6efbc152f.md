base-class pointer. All of these calls are legitimate, because BasePlusCommissionEmployee inherits these member functions from CommissionEmployee. We know that commissionEmployeePtr is aimed at a BasePlusCommissionEmployee object, so in lines 26–27 we attempt to invoke BasePlusCommissionEmployee member functions getBaseSalary and setBaseSalary. The compiler generates errors on both of these calls, because they're not made to member functions of base-class CommissionEmployee. The handle can be used to invoke only those functions that are members of that handle's associated class type. (In this case, off a CommissionEmployee *, we can invoke only CommissionEmployee member functions setFirstName, getFirstName, setLastName, getLastName, setSocialSecurityNumber, getSocialSecurityNumber, setGrossSales, getGrossSales, setCommissionRate, getCommissionRate, earnings and print.)

```
```cpp
1   // Fig. 13.7: fig13_07.cpp
2   // Attempting to invoke derived-class-only member functions
3   // through a base-class pointer.
4   #include "CommissionEmployee.h"
5   #include "BasePlusCommissionEmployee.h"
6
7   int main()
8   {
9      CommissionEmployee *commissionEmployeePtr = 0; // base class
10     BasePlusCommissionEmployee basePlusCommissionEmployee(
11        "Bob", "Lewis", "333-33-3333", 5000, .04, 300 ); // derived class
12
13     // aim base-class pointer at derived-class object
14     commissionEmployeePtr = &basePlusCommissionEmployee;
15
16     // invoke base-class member functions on derived-class
17     // object through base-class pointer (allowed)
18     string firstName = commissionEmployeePtr->getFirstName();
19     string lastName = commissionEmployeePtr->getLastName();
20     string ssn = commissionEmployeePtr->getSocialSecurityNumber();
21     double grossSales = commissionEmployeePtr->getGrossSales();
22     double commissionRate = commissionEmployeePtr->getCommissionRate();
23
24     // attempt to invoke derived-class-only member functions
25     // on derived-class object through base-class pointer (disallowed)
26     double baseSalary = commissionEmployeePtr->getBaseSalary();
27     commissionEmployeePtr->setBaseSalary( 500 );
28  } // end main
```
```

*Microsoft Visual C++ compiler error messages:*

```
```
C:\cpphtp7_examples\ch13\Fig13_07\Fig13_07.cpp(26) : error C2039:
   'getBaseSalary' : is not a member of 'CommissionEmployee'
   C:\cpphtp7_examples\ch13\Fig13_07\CommissionEmployee.h(10) :
      see declaration of 'CommissionEmployee'
C:\cpphtp7_examples\ch13\Fig13_07\Fig13_07.cpp(27) : error C2039:
   'setBaseSalary' : is not a member of 'CommissionEmployee'
   C:\cpphtp7_examples\ch13\Fig13_07\CommissionEmployee.h(10) :
      see declaration of 'CommissionEmployee'
```
```

**Fig. 13.7** | Attempting to invoke derived-class-only functions via a base-class pointer. (Part 1 of 2.)