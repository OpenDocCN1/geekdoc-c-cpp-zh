The virtual function `print` (lines 53–57) provides an *implementation* that will be *overridden* in each of the derived classes. Each of these functions will, however, use the abstract class's version of `print` to print information *common* to all classes in the `Employee` hierarchy.

# 20.6.2 Creating Concrete Derived Class SalariedEmployee

Class `SalariedEmployee` (Figs. 20.11–20.12) derives from class `Employee` (line 9 of Fig. 20.11). The `public` member functions include a constructor that takes a first name, a last name, a social security number and a weekly salary as arguments (lines 12–13); a virtual destructor (line 14); a `set` function to assign a new nonnegative value to data member `weeklySalary` (line 16); a `get` function to return `weeklySalary`'s value (line 17); a virtual function `earnings` that calculates a `SalariedEmployee`'s earnings (line 20) and a virtual function `print` (line 21) that outputs the employee's type, namely, "salaried employee," followed by employee-specific information produced by base class `Employee`'s `print` function and `SalariedEmployee`'s `getWeeklySalary` function.

```
~~~cpp
1  // Fig. 20.11: SalariedEmployee.h
2  // SalariedEmployee class derived from Employee.
3  #ifndef SALARIED_H
4  #define SALARIED_H
5  
6  #include <string> // C++ standard string class
7  #include "Employee.h" // Employee class definition
8  
9  class SalariedEmployee : public Employee
10 {
11 public:
12    SalariedEmployee( const std::string &, const std::string &,
13       const std::string &, double = 0.0 );
14    virtual ~SalariedEmployee() { } // virtual destructor
15  
16    void setWeeklySalary( double ); // set weekly salary
17    double getWeeklySalary() const; // return weekly salary
18  
19    // keyword virtual signals intent to override
20    virtual double earnings() const override; // calculate earnings
21    virtual void print() const override; // print object
22 private:
23    double weeklySalary; // salary per week
24 }; // end class SalariedEmployee
25  
26 #endif // SALARIED_H
~~~
```

**Fig. 20.11** | SalariedEmployee class header.

# *SalariedEmployee Class Member-Function Definitions*

Figure 20.12 contains the member-function definitions for `SalariedEmployee`. The class's constructor passes the first name, last name and social security number to the `Employee` constructor (line 11) to initialize the private data members that are inherited from the base class, but not directly accessible in the derived class. Function `earnings`