

For another example where inheritance can be applied, consider the CD account in Chapter 10. We discussed how a CD account is a more specialized version of a savings account. By deriving the class CDAccount from SavingsAccount, we automatically inherit all of the SavingsAccount public functions and variables when we create a CDAccount object. C++ uses inheritance in predefined classes as well. In using streams for file I/O, the predefined class ifstream is derived from the (predefined) class istream by adding member functions such as open and close. The stream cin belongs to the class of all input streams (that is, the class istream), but it does not belong to the class of input-file streams (that is, does not belong to ifstream), partly because it lacks the member functions open and close of the derived class ifstream.

## Derived Classes

Suppose we are designing a record-keeping program that has records for salaried employees and hourly employees. There is a natural hierarchy for grouping these classes. These are all classes of people who share the property of being employees.

Employees who are paid an hourly wage are one subset of employees. Another subset consists of employees who are paid a fixed wage each month or each week. Although the program may not need any type corresponding to the set of all employees, thinking in terms of the more general concept of employees can be useful. For example, all employees have names and Social Security numbers, and the member functions for setting and changing names and Social Security numbers will be the same for salaried and hourly employees.

Within C++ you can define a class called Employee that includes all employees, whether salaried or hourly, and then use this class to define classes for hourly employees and salaried employees. Displays 15.2 and 15.3 show one possible definition for the class Employee.

You can have an (undifferentiated) Employee object, but our reason for defining the class Employee is so that we can define derived classes for different kinds of employees. In particular, the function printCheck will always have its definition changed in derived classes so that different kinds of employees can have different kinds of checks. This is reflected in the definition of the function printCheck for the class Employee (Display 15.3). It makes little sense to print a check for such an (undifferentiated) Employee. We know nothing about this employee’s salary details. Consequently, we implemented the function printCheck of the class Employee so that the program stops with an error message if printCheck is called for a base class Employee object. As you will see, derived classes will have enough information to redefine the function printCheck to produce meaningful employee checks.

A class that is derived from the class Employee will automatically have all the member variables of the class Employee (name, ssn, and netPay). A class that is derived from the class Employee will also have all the member functions of the class Employee, such as printCheck, getName, setName, and the other

member functions listed in Display 15.2. This is usually expressed by saying that the derived class inherits the member variables and member functions.

The interface files with the class definitions of two derived classes of the class Employee are given in Displays 15.4 (HourlyEmployee) and 15.5 (SalariedEmployee). We have placed the class Employee and the two derived classes in the same namespace. C++ does not require that they be in the same namespace, but since they are related classes, it makes sense to put them there. We will first discuss the derived class HourlyEmployee given in Display 15.4.

Note that the definition of a derived class begins like any other class definition but adds a colon, the reserved word public, and the name of the base

### DISPLAY 15.2 Interface for the Base Class Employee

```
//This is the header file employee.h.
//This is the interface for the class Employee.
//This is primarily intended to be used as a base class to derive
//classes for different kinds of employees.
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>
using namespace std;

namespace employeeessavitch
{

    class Employee
    {
    public:
        Employee();
        Employee(string theName, string theSSN);
        string getName() const;
        string getSSN() const;
        double getNetPay() const;
        void setName(string newName);
        void setSSN(string newSSN);
        void setNetPay(double newNetPay);
        void printCheck() const;
    private:
        string name;
        string ssn;
        double netPay;
    };

}//employeeessavitch

#endif //EMPLOYEE_H
```

### DISPLAY 15.4 Interface for the Derived Class HourlyEmployee (part 2 of 2)

```
20     void printCheck();
21     private:
22         double wageRate;
23         double hours;
24     };
25 } // employeeessavitch
26 #endif // HOURLY EMPLOYEE_H
```

> You only list the declaration of an inherited member function if you want to change the definition of the function.

### DISPLAY 15.5 Interface for the Derived Class SalariedEmployee

```
// This is the header file salariedemployee.h.
// This is the interface for the class SalariedEmployee.
#ifndef SALARIEDEMPLOYEE_H
#define SALARIEDEMPLOYEE_H

#include <string>
#include "employee.h"

using namespace std;

namespace employeeessavitch
{

    class SalariedEmployee : public Employee
    {
    public:
        SalariedEmployee();
        SalariedEmployee(string theName, string theSSN, double theWeeklySalary);
        double getSalary() const;
        void setSalary(double newSalary);
        void printCheck();
    private:
        double salary; // weekly
    };

} // employeeessavitch

#endif // SALARIEDEMPLOYEE_H
```

class to the first line of the class definition, as in the following (from Display 15.4):

```
class HourlyEmployee : public Employee
{
```

By using the keyword public the derived class (such as HourlyEmployee) automatically receives all the public member variables and member functions of the base class (such as Employee). We can also add additional member variables and member functions to the derived class.

The definition of the class HourlyEmployee does not mention the member variables name, ssn, and netPay, but every object of the class HourlyEmployee has member variables named name, ssn, and netPay. These member variables are inherited from the class Employee. The class HourlyEmployee declares two additional member variables named wageRate and hours. Thus, every object of the class HourlyEmployee has five member variables named name, ssn, netPay, wageRate, and hours. Note that the definition of a derived class (such as HourlyEmployee) only lists the added member variables. The member variables defined in the base class are not mentioned. They are provided automatically to the derived class.

Just as it inherits the member variables of the class Employee, the class HourlyEmployee inherits all the member functions from the class Employee. So, the class HourlyEmployee inherits the member functions getName, getSSN, getNetPay, setName, setSSN, setNetPay, and printCheck from the class Employee.

In addition to the inherited member variables and member functions, a derived class can add new member variables and new member functions. The new member variables and the declarations for the new member functions are listed in the class definition. For example, the derived class HourlyEmployee adds the two member variables wageRate and hours, and it adds the new member functions named setRate, getRate, setHours, and getHours. This is shown in Display 15.4. Note that you do not give the declarations of the inherited member functions except for those whose definitions you want to change, which is the reason we list only the member function printCheck from the base class Employee. For now, do not worry about the details of the constructor definition for the derived class. We will discuss constructors in the next subsection.

In the implementation file for the derived class, such as the implementation of HourlyEmployee in Display 15.6, you give the definitions of all the added member functions. Note that you do not give definitions for the inherited member functions unless the definition of the member function is changed in the derived class, a point we discuss next.

The definition of an inherited member function can be changed in the definition of a derived class so that it has a meaning in the derived class that is different from what it is in the base class. This is called redefining the inherited member function. For example, the member function printCheck( ) is redefined in the definition of the derived class HourlyEmployee. To redefine a

