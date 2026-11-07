
## An Inheritance Example in Code

To demonstrate how inheritance works in C++, we'll develop a set of classes that simulate the relationship between the different types of employees in a company.

For the sake of this demonstration, we will define three types of employees in a company – a regular employee, a supervisor, and a manager. We'll make the Employee class the base class, and the Supervisor class and the Manager class will be derived classes.

First, let's define the Employee class. To keep things from getting too complicated, we'll define all the classes within the same program. We don't advocate doing that in "real world" programs, but it will make our discussion easier to follow if all the class definitions are in the same place.

Here is a first stab at defining an Employee class and a test program to test the implementation:

```cpp
// EmployeeClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Employee
{
private:
        string empName;
        double pay;

public:
        Employee(string name, double payRate)
        {
                empName = name;
                pay = payRate;
        }

        string getName()
        {
            return empName;
        }

        double getPay()
        {
            return pay;
        }

        double grossPay(int hours)
        {
            return pay * hours;
        }
};

int main(array<System::String ^> ^args)
{
    Employee emp1("Mary Smith", 15.0);
    cout << "Employee name: " << emp1.getName() << endl;
    cout << "Pay rate: " << emp1.getPay() << endl;
    cout << "Gross pay: " << emp1.grossPay(40) << endl;
    Console::ReadKey();
    return 0;
}
```

The output from this program is:

```
Employee name: Mary Smith
Pay rate: 15
Gross pay: 600
```

Now we're ready to derive the Manager class from the Employee class. When we derive a class from a base class, we want to implement just the different members and methods that occur in the derived class and reuse the members and methods of the base class that are shared with the derived class. This means that we want to continue to use the data members from the Employee class in the Manager class and add any attribute that is different, such as the fact that managers are usually salaried employees rather than hourly employees. We can add this fact to the Manager class by including a boolean variable, isSalaried, and then adjusting the grossPay() method to return either the pay rate if the object is a manager or the pay rate multiplied by the hours worked if the object is a regular employee.

We're almost ready to implement the Manager class, but there is one major problem. The data members of the Employee class are private members, meaning that their values are only accessible within the class definition. There is an access modifier we can use for base classes so that the members and methods of the class are accessible to a derived class: protected. This access modifier allows derived classes to access members and methods of a base class but does not allow access by any other code, such as a test program.

Once we've made the members and methods of the base class, we have to tell the compiler that the derived class is inheriting members and methods from a base class. To do this, include a reference to the base class by writing a colon followed by the keyword public and the base class name on the same line as the first line of the derived class definition, like this:

```cpp
class Manager : public Employee
```

Now we're ready to redefine the Employee class and define the Manager class. Here is the complete program:

```cpp
// EmployeeClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Employee
{
protected:
    string empName;
    double pay;

public:
    Employee(string name, double payRate)
    {
        empName = name;
        pay = payRate;
    }

    string getName()
    {
        return empName;
    }

    double getPay()
    {
        return pay;
    }

    double grossPay(int hours)
    {
        return pay * hours;
    }
};

class Manager : public Employee
{
protected:
    bool salaried;

public:
    Manager(string name, double payRate,
            bool isSalaried)
        : Employee(name, payRate)
    {
        salaried = isSalaried;
    }

    bool getSalaried()
    {
        return salaried;
    }

    double grossPay(double hours)
    {
        if (salaried)
            return pay;
        else
            return Employee::grossPay(hours);
    }
};

int main(array<System::String ^> ^args)
{
    Employee emp1("Mary Smith", 15.0);
    cout << "Employee name: " << emp1.getName()
         << endl;
    cout << "Pay rate: " << emp1.getPay() << endl;
    cout << "Gross pay: " << emp1.grossPay(40)
         << endl;
    Manager emp2("Liz Warren", 1500, true);
    cout << "Employee name: " << emp2.getName()
         << endl;
    cout << "Pay rate: " << emp2.getPay() << endl;
    cout << "Gross pay: " << emp2.grossPay(40)
         << endl;
    Console::ReadKey();
    return 0;
}
```

The first change we made was changing the access modifier of the Employee class data members from private to protected. Here is that section of code:

```cpp
class Employee
{
protected:
    string empName;
    double pay;
```

This change had to be made in order for the data members of the Employee class to be accessible by the Manager class. Because of this we don't have to re-declare the data members from the Employee class in the Manager class.

The constructor for the Manager class also takes advantage of inheritance by using the member assignments from the Employee class definition for the employee name and the employee pay. Let's focus just on the constructor to see how it works:

```cpp
Manager(string name, double payRate,
        bool isSalaried)
    : Employee(name, payRate)
{
    salaried = isSalaried;
}
```

The parameter list for the constructor includes parameters for all the data members. After the list, though, there is a colon followed by a call to the base class constructor for the Employee class. Think of this like a function call. At this point in the code, the compiler transfers control to the code defined for the Employee class constructor. This is a classic example of code reuse and one of the most important features of inheritance. There is no reason to include the statements:

```
empName = name;
pay = payRate;
```

since we've already written them in the base class.

The rest of the constructor body assigns the last parameter to the new data member of the Manager class, the boolean data member salaried.

The other piece of code that requires explanation is the grossPay() method. Here is the definition again:

```cpp
double grossPay(double hours)
{
    if (salaried)
        return pay;
    else
        return Employee::grossPay(hours);
}
```

This method first checks to see if the employee is being paid a salary by testing the salaried variable. If so, the method just returns the value in pay. If the employee is not salaried, the method computes the gross pay. Since we already performed this computation in the Employee class, there is no reason to repeat it in the Manager class. Instead, we just use that method directly from the Employee class by calling it like this:

`Employee::grossPay(hours)`

If we had just written:

`grossPay(hours)`

the compiler would get confused and call the same method again, leading to a never-ending recursive call that would eventually crash the program. This example demonstrates how using inheritance in C++ can help reduce the amount of code you have to write, leading to code that is easier to use and easier to debug.

### Composition

Inheritance is the reuse of the code from a base class in a derived class. *Composition* is the use of other classes in the definition of a class. Composition is used to describe *has-a* relationships. A line has a point (well, two points to be exact); a circle has a radius; a car has an engine. These are all examples of an object that is composed of other objects.

Many programming problems that seem to lend themselves to an inheritance solution are actually better solved by using composition. Inheritance, especially when involving long chains of derived classes, is notoriously hard to get correct.
