# Inheritance Basics

Display 14.4 Interface for the Derived Class SalariedEmployee

```
1
2 //This is the header file salariedemployee.h.
3 //This is the interface for the class SalariedEmployee.
4 #ifndef SALARIEDEMPLOYEE_H
5 #define SALARIEDEMPLOYEE_H

6 #include <string>
7 #include "employee.h"

8 using std::;

9 namespace SavitchEmployees
10 {

11     class SalariedEmployee : public Employee
12     {
13         public:
14             SalariedEmployee();
15             SalariedEmployee(const string&theName, const string&theSsn,
16                             doubleWeeklySalary());
17             double getSalary() const;
18             void setSalary(double new);
19             void printCheck();
20     private:
21             double salary;//weekly
22     };

23 //SavitchEmployees
24 #endif SALARIEDEMPLOYEE_H
```

has member variables named name, ssn, and netPay. The member variables name, ssn, and netPay are inherited from the class Employee. The class HourlyEmployee declares two additional member variables named wageRate and hours. Thus, every object of the class HourlyEmployee has five member variables named name, ssn, netPay, wageRate, and hours. Note that the definition of a derived class (such as HourlyEmployee) lists only the added member variables. The member variables defined in the base class are not mentioned. They are automatically provided to the derived class.
Just as it inherits the member variables of the class Employee, so too the class HourlyEmployee inherits all the member functions from the class Employee. Thus, the class HourlyEmployee inherits the member functions getName, getSsn, getNetPay, setName, setSsn, setNetPay, and printCheck from the class Employee.