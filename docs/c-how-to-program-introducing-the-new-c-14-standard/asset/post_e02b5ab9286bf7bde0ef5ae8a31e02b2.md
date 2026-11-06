
```cpp
}

// set gross sales amount
void CommissionEmployee::setGrossSales(double sales) {
    if (sales < 0.0) {
        throw invalid_argument("Gross sales must be >= 0.0");
    }

    grossSales = sales;
}

// return gross sales amount
double CommissionEmployee::getGrossSales() const { return grossSales; }

// set commission rate
void CommissionEmployee::setCommissionRate(double rate) {
    if (rate <= 0.0 || rate >= 1.0) {
        throw invalid_argument("Commission rate must be > 0.0 and < 1.0");
    }

    commissionRate = rate;
}

// return commission rate
double CommissionEmployee::getCommissionRate() const {
    return commissionRate;
}

// calculate earnings
double CommissionEmployee::earnings() const {
    return getCommissionRate() * getGrossSales();
}

// return string representation of CommissionEmployee object
string CommissionEmployee::toString() const {
    ostringstream output;
    output << fixed << setprecision(2); // two digits of precision
    output << "commission employee: "
        << getFirstName() << " " << getLastName()
        << "\nsocial security number: " << getSocialSecurityNumber()
        << "\ngross sales: " << getGrossSales()
        << "\ncommission rate: " << getCommissionRate();
    return output.str();
}
```

Fig. 11.14 **CommissionEmployee** class implementation file: **CommissionEmployee** class uses member functions to manipulate its *private* data.

In the body of the constructor and in the bodies of member functions `earnings` (Fig. 11.14, lines 70–72) and `toString` (lines 75–84), we call the class’s set and get member functions to access the class’s `private` data members. If we decide to change the data member names, the `earnings` and `toString` definitions will *not* require modification—only the definitions of the get and set member functions that directly manipulate the data members will need to change. *These changes occur solely within the base class—no changes to the derived class are needed.* Localizing the effects of changes like this is a good software engineering practice.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1507_0.png)

## Performance Tip 11.2

*Using a member function to access a data member’s value can be slightly slower than accessing the data directly. However, today’s optimizing compilers perform many optimizations implicitly (such as inlining set and get member-function calls). You should write code that adheres to proper software engineering principles, and leave optimization to the compiler. A good rule is, “Do not second-guess the compiler.”*

## Changes to Class `BasePlusCommissionEmployee`’s Member-Function Definitions

Class `BasePlusCommissionEmployee` inherits `CommissionEmployee`’s `public` member functions and can access the `private` base-class members via the inherited member functions. The class’s header remains unchanged from Fig. 11.10. The class has several changes to its member-function implementations (Fig. 11.15) that distinguish it from the previous version of the class (Figs. 11.10–11.11). Member functions `earnings` (Fig. 11.15, lines 32–34) and `toString` (lines 37–42) each invoke member function `getBaseSalary` to obtain the base salary value, rather than accessing `baseSalary` directly. This insulates `earnings` and `toString` from potential changes to the implementation of data member `baseSalary`. For example, if we decide to rename data member `baseSalary` or change its type, only member functions `setBaseSalary` and `getBaseSalary` will need to change.

```cpp
// Fig. 11.15: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <stdexcept>
#include <sstream>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
   const string& first, const string& last, const string& ssn,
   double sales, double rate, double salary)
   // explicitly call base-class constructor
   : CommissionEmployee(first, last, ssn, sales, rate) {
   setBaseSalary(salary); // validate and store base salary
}

// set base salary
void BasePlusCommissionEmployee::setBaseSalary(double salary) {
   if (salary < 0.0) {
      throw invalid_argument("Salary must be >= 0.0");
   }

   baseSalary = salary;
}

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const {
   return baseSalary;
}

// calculate earnings
double BasePlusCommissionEmployee::earnings() const {
   return getBaseSalary() + CommissionEmployee::earnings();
}

// return string representation of BasePlusCommissionEmployee object
string BasePlusCommissionEmployee::toString() const {
   ostringstream output;
   output << "base-salaried " << CommissionEmployee::toString()
      << "\nbase salary: " << getBaseSalary();
   return output.str();
}
```

**Fig. 11.15** `BasePlusCommissionEmployee` class that inherits from class `CommissionEmployee` but cannot directly access the class’s `private` data.

## `BasePlusCommissionEmployee` Member Function `earnings`

Class `BasePlusCommissionEmployee`’s `earnings` function (Fig. 11.15, lines 32–34) redefines class `CommissionEmployee`’s `earnings` member function (Fig. 11.14, lines 70–72) to calculate the earnings of a `BasePlusCommissionEmployee`. Class `BasePlusCommissionEmployee`’s version of `earnings` obtains the portion of the employee’s earnings based on commission alone by calling base-class `CommissionEmployee`’s `earnings` function with the expression `CommissionEmployee::earnings()` as shown in line 33 of Fig. 11.15. `BasePlusCommissionEmployee`’s `earnings` function then adds the base salary to this value to calculate the total earnings of the employee. Note the syntax used to invoke a redefined base-class member function from a derived class—place the base-class name and the scope resolution operator (`::`) before the base-class member-function name. This member-function invocation is a good software engineering practice: Recall from Chapter 9 that, if an object’s member function performs the actions needed by another object, we should call that member function rather than duplicating its code body. By having `BasePlusCommissionEmployee`’s `earnings` function invoke `CommissionEmployee`’s `earnings` function to calculate part of a `BasePlusCommissionEmployee` object’s earnings, we avoid duplicating the code and reduce code-maintenance problems.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1511_0.png)

## Common Programming Error 11.2

When a base-class member function is redefined in a derived class, the derived-class version often calls the base-class version to do additional work. Failure to use the `::` operator prefixed with the name of the base class when referencing the base class’s member function causes infinite recursion, because the derived-class member function would then call itself.

## `BasePlusCommissionEmployee` Member Function `toString`

Similarly, `BasePlusCommissionEmployee`’s `toString` function (Fig. 11.15, lines 37–42) redefines class `CommissionEmployee`’s `toString` function (Fig. 11.14, lines 75–84) to output the appropriate base-salaried commission employee information. The new version displays "base-salaried" followed by the part of a `BasePlusCommissionEmployee` object’s information returned by calling `CommissionEmployee`’s `toString` member function with the qualified name `CommissionEmployee::toString()` (Fig. 11.15, line 39)—this returns a `string` containing "commission employee" and the values of class `CommissionEmployee`’s `private` data members. `BasePlusCommissionEmployee`’s `toString` function then outputs the remainder of a `BasePlusCommissionEmployee` object’s information (i.e., the value of class `BasePlusCommissionEmployee`’s base salary preceded by "base salary:").

## *Testing the Modified Class Hierarchy*

Once again, this example uses the `BasePlusCommissionEmployee` test program from [Fig. 11.9](#) and produces the same output. Although each “base-salaried commission employee” class behaves identically, the version in this example is the best engineered. *By using inheritance and by calling member functions that hide the data and ensure consistency, we’ve efficiently and effectively constructed a well-engineered class.*
