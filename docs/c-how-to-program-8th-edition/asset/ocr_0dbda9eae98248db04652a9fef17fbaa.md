```
```cpp
52    << "function on that derived-class object: \n\n";
53    commissionEmployeePtr->print(); // invokes base-class print
54    cout << endl;
55 } // end main
```
```

```
```text
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

Calling print with derived-class pointer to
derived-class object invokes derived-class print function:

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
commission rate: 0.04
```
```

**Fig. 13.1 |** Assigning addresses of base-class and derived-class objects to base-class and derived-class pointers. (Part 2 of 2.)

Recall that each BasePlusCommissionEmployee object is a CommissionEmployee that also has a base salary. Class BasePlusCommissionEmployee’s earnings member function (lines 33–36 of Fig. 12.15) redefines class CommissionEmployee’s earnings member function (lines 84–87 of Fig. 12.14) to include the object’s base salary. Class BasePlusCommissionEmployee’s print member function (lines 39–47 of Fig. 12.15) redefines class CommissionEmployee’s version (lines 90–97 of Fig. 12.14) to display the same information plus the employee’s base salary.