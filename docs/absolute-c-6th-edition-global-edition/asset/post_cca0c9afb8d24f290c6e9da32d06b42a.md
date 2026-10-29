
setting and changing names and Social Security numbers will be the same for salaried and hourly employees.

Within C++ you can define a class called Employee that includes all employees, whether salaried or hourly and then use this class to define classes for hourly employees and salaried employees.

The class Employee will also contain member functions that manipulate the data fields of the class Employee. Displays 14.1 and 14.2 show one possible definition for the class Employee.

## Display 14.1 Interface for the Base Class Employee

```
//This is the header file employee.h.
//This is the interface for the class Employee.
//This is primarily intended to be used as a base class to derive
//classes for different kinds of employees.
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>
using std::string;

namespace SavitchEmployees
{

class Employee
{
public:
Employee();
Employee(const string& theName, const string& theSsn);
string getName() const;
string getSsn() const;
double getNetPay() const;
void setName(const string& newName);
void setSsn(const string& newSsn);
void setNetPay(double newNetPay);
void printCheck() const;
private:
string name;
string ssn;
double netPay;
};

};//SavitchEmployees

#endif //EMPLOYEE_H
```

## Display 14.2 Implementation for the Base Class Employee (part 1 of 2)

```
//This is the file employee.cpp.
//This is the implementation for the class Employee.
//The interface for the class Employee is in the header file employee.h.
#include <string>
#include <cstdlib>
#include <iostream>
#include "employee.h"
using std::string;
using std::cout;

namespace SavitchEmployees
{
    Employee::Employee() : name("No name yet"), ssn("No number yet"), netPay(0)
    {
        //deliberately empty
    }

    Employee::Employee(const string& theName, const string& theNumber)
        : name(theName), ssn(theNumber), netPay(0)
    {
        //deliberately empty
    }

    string Employee::getName() const
    {
        return name;
    }

    string Employee::getSsn() const
    {
        return ssn;
    }

    double Employee::getNetPay() const
    {
        return netPay;
    }

    void Employee::setName(const string& newName)
    {
        name = newName;
    }

    void Employee::setSsn(const string& newSsn)
```

## Display 14.2 Implementation for the Base Class Employee (part 2 of 2)

```
{
    ssn = newSsn;
}

void Employee::setNetPay (double newNetPay)
{
    netPay = newNetPay;
}

void Employee::printCheck( ) const
{
    cout << "\nERROR: printCheck FUNCTION CALLED FOR AN \n"
         << "UNDIFFERENTIATED EMPLOYEE. Aborting the program.\n"
         << "Check with the author of the program about this bug.\n";
    exit(1);
}
}//SavitchEmployees
```

You can have an (undifferentiated) Employee object, but our reason for defining the class Employee is so that we can define derived classes for different kinds of employees. In particular, the function printCheck will always have its definition changed in derived classes so that different kinds of employees can have different kinds of checks. This is reflected in the definition of the function printCheck for the class Employee (Display 14.2). It makes little sense to print a check for such an (undifferentiated) Employee. We know nothing about this employee. Consequently, we implemented the function printCheck of the class Employee so that the program stops with an error message if printCheck is called for a base class Employee object. As you will see, derived classes will have enough information to redefine the function printCheck to produce meaningful employee checks.

A class that is derived from the class Employee will automatically have all the member variables of the class Employee (name, ssn, and netPay). A class that is derived from the class Employee will also have all the member functions of the class Employee, such as printCheck, getName, setName, and the other member functions listed in Display 14.1. This is usually expressed by saying that the derived class inherits the member variables and member functions.

The interface files with the class definitions of two derived classes of the class Employee are given in Displays 14.3 (HourlyEmployee) and 14.4 (SalariedEmployee). We have placed the class Employee and the two derived classes in the same namespace. C++ does not require that they be in the same namespace, but since they are related classes, it makes sense to put them in the same namespace. We will first discuss the derived class HourlyEmployee, given in Display 14.3.

## Display 14.3 Interface for the Derived Class HourlyEmployee

```
//This is the header file hourlyemployee.h.
//This is the interface for the class HourlyEmployee.
#ifndef HOURLYEMPLOYEE_H
#define HOURLYEMPLOYEE_H

#include <string>
#include "employee.h"

using std::string;

namespace SavitchEmployees
{

class HourlyEmployee : public Employee
{
public:
    HourlyEmployee();
    HourlyEmployee(const string& theName, const string& theSsn, double theWageRate, double theHours);
    void setRate(double newWageRate);
    double getRate() const;
    void setHours(double hoursWorked);
    double getHours() const;
    void printCheck();
private:
    double wageRate;
    double hours;
};

}//SavitchEmployees

#endif //HOURLYEMPLOYEE_H
```

Note that the definition of a derived class begins like any other class definition but adds a colon, the reserved word public, and the name of the base class to the first line of the class definition, as in the following (from Display 14.3):

```
class HourlyEmployee : public Employee
{
```

The derived class (such as HourlyEmployee) automatically receives all the member variables and member functions of the base class (such as Employee) and can add additional member variables and member functions.

The definition of the class HourlyEmployee does not mention the member variables name, ssn, and netPay, but every object of the class HourlyEmployee has

> List only the declaration of an inherited member function if you want to change the definition of the function.

## Display 14.4 Interface for the Derived Class SalariedEmployee

```
//This is the header file salariedemployee.h.
//This is the interface for the class SalariedEmployee.
#ifndef SALARIEDEMPLOYEE_H
#define SALARIEDEMPLOYEE_H

#include <string>
#include "employee.h"

using std::string;

namespace SavitchEmployees
{

class SalariedEmployee : public Employee
{
public:
    SalariedEmployee();
    SalariedEmployee(const string& theName, const string& theSsn,
                    double theWeeklySalary);
    double getSalary() const;
    void setSalary(double newSalary);
    void printCheck();
private:
    double salary;//weekly
};
}//SavitchEmployees

#endif //SALARIEDEMPLOYEE_H
```

member variables named name, ssn, and netPay. The member variables name, ssn, and netPay are inherited from the class Employee. The class HourlyEmployee declares two additional member variables named wageRate and hours. Thus, every object of the class HourlyEmployee has five member variables named name, ssn, netPay, wageRate, and hours. Note that the definition of a derived class (such as HourlyEmployee) lists only the added member variables. The member variables defined in the base class are not mentioned. They are provided automatically to the derived class.

Just as it inherits the member variables of the class Employee, so too the class HourlyEmployee inherits all the member functions from the class Employee. Thus, the class HourlyEmployee inherits the member functions getName, getSsn, getNetPay, setName, setSsn, setNetPay, and printCheck from the class Employee.

## Inherited Members

A derived class automatically has all the member variables and all the ordinary member functions of the base class. (As discussed later in this chapter, there are some specialized member functions, such as constructors, that are not automatically inherited.) These members from the base class are said to be inherited. These inherited member functions and inherited member variables are, with one exception, not mentioned in the definition of the derived class but are automatically members of the derived class. As explained in the text, you do mention an inherited member function in the definition of the derived class if you want to change the definition of the inherited member function.

In addition to the inherited member variables and member functions, a derived class can add new member variables and new member functions. The new member variables and the declarations for the new member functions are listed in the class definition. For example, the derived class HourlyEmployee adds the two member variables wageRate and hours and adds the new member functions setRate, getRate, setHours, and getHours. This is shown in Display 14.3. Note that you do not give the declarations of the inherited member functions unless you want to change these definitions, which is a point that we will discuss shortly. For now, do not worry about the details of the constructor definition for the derived class. We will discuss constructors in the next subsection.

In the implementation file for the derived class, such as the implementation of HourlyEmployee in Display 14.5, give the definitions of all the added member functions. Note that you do not give definitions for the inherited member functions unless the definition of the member function is changed in the derived class, a point we discuss next.

## Parent and Child Classes

When discussing derived classes, it is common to use terminology derived from family relationships. A base class is often called a parent class. A derived class is then called a child class. This makes the language of inheritance very smooth. For example, we can say that a child class inherits member variables and member functions from its parent class. This analogy is often carried one step further. A class that is a parent of a parent of another class (or some other number of "parent of" iterations) is often called an ancestor class. If class A is an ancestor of class B, then class B is often called a descendant of class A.

The definition of an inherited member function can be changed in the definition of a derived class so that it has a meaning in the derived class that is different from what it is in the base class. This is called redefining the inherited member function. For example, the member function printCheck() is redefined in the definition of the derived class HourlyEmployee. To redefine a member function definition, simply
