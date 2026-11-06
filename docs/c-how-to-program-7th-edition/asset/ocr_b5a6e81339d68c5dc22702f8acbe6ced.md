nor does it provide a baseSalary data member to set. This could lead to problems, because member function setBaseSalary would assume that there is a baseSalary data member to set at its “usual location” in a BasePlusCommissionEmployee object. This memory does not belong to the CommissionEmployee object, so member function setBaseSalary might overwrite other important data in memory, possibly data that belongs to a different object.

```
~~~cpp
1 // Fig. 13.6: fig13_06.cpp
2 // Aiming a derived-class pointer at a base-class object.
3 #include "CommissionEmployee.h"
4 #include "BasePlusCommissionEmployee.h"
5
6 int main()
7 {
8    CommissionEmployee employee(
9       "Sue", "Jones", "222-22-2222", 10000, .06 );
10   BasePlusCommissionEmployee *basePlusCommissionEmployeePtr = 0;
11
12   // aim derived-class pointer at base-class object
13   // Error: a CommissionEmployee is not a BasePlusCommissionEmployee
14   basePlusCommissionEmployeePtr = &employee;
15 } // end main
~~~
```

*Microsoft Visual C++ compiler error message:*

```
~~~
C:\\cpphtp7_examples\\ch13\\Fig13_06\\fig13_06.cpp(14) : error C2440: '=' :
cannot convert from 'CommissionEmployee *' to 'BasePlusCommissionEmployee *'
        Cast from base to derived requires dynamic_cast or static_cast
~~~
```

*GNU C++ compiler error message:*

```
~~~
fig13_06.cpp:14: error: invalid conversion from 'CommissionEmployee*' to 'BasePlusCommissionEmployee*'
~~~
```

**Fig. 13.6** | Aiming a derived-class pointer at a base-class object.

# ### 13.3.3 Derived-Class Member-Function Calls via Base-Class Pointers

Off a base-class pointer, the compiler allows us to invoke only base-class member functions. Thus, if a base-class pointer is aimed at a derived-class object, and an attempt is made to access a derived-class-only member function, a compilation error will occur.

Figure 13.7 shows the consequences of attempting to invoke a derived-class member function off a base-class pointer. [Note: We are again using classes CommissionEmployee and BasePlusCommissionEmployee of Figs. 13.1–13.4.] Line 9 creates commissionEmployeePtr—a pointer to a CommissionEmployee object—and lines 10–11 create a BasePlusCommissionEmployee object. Line 14 aims commissionEmployeePtr at derived-class object basePlusCommissionEmployee. Recall from Section 13.1 that this is allowed, because a BasePlusCommissionEmployee is a CommissionEmployee (in the sense that a BasePlusCommissionEmployee object contains all the functionality of a CommissionEmployee object). Lines 18–22 invoke base-class member functions getFirstName, getLastName, getSocialSecurityNumber, getGrossSales and getCommissionRate off the