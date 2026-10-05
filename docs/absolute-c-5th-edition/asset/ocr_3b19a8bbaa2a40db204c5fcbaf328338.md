# CHAPTER 15 Polymorphism and Virtual Functions

# EXAMPLE: An Abstract Class

In Display 15.6, we have slightly rewritten the class Employee from Display 14.1. This time we have made Employee an abstract class. The following line (highlighted \in Display 15.6) is the only thing that is different from our previous definition of Employee (Display 14.1):

```
virtual void printCheck() ) const =;
```

The word virtual and the = in the member function telling the compiler that is a pure virtual function and therefore the class Employee is now an abstract class. The implementation for the class Employee includes no definition for the class Employee::printCheck, but otherwise the implementation of the class Employee is the same as before (that is, the same as in Display 14.2).
It senses that there is no definition for the member function Employee::printCheck, since you know not what kind of check to write until what kind of employee you are dealing. In our first definition of the class Employee (Displays 14.1 and 14.2), we were forced to give a definition to Employee::printCheck and so gave that an error message saying that the function should not be invoked. We have a more elegant solution. by making Employee::printCheck a pure virtual function, we have set things up that the compiler will enforce the ban against invoking Employee::printCheck.

Display 15.6 Interface for the Abstract Class Employee (part 1 of 2)

```
1 //This is the header file employee.h.
2 //This is the interface for the abstract class Employee.
4 #ifndef EMPLOYEE_H
5 #define EMPLOYEE_H

6 #include <string>
7 using std::string;
8 namespace SavitchEmployees
9 {
10 class Employee
11 public:
12 Employee();
13 Employee(const string&tName, const string&tSsn);
14 string getName() const;
15 string getSsn() const;
16 double getPay() const;
17 void setName(const string&newName);
```

> This is an improved version of the class
Employee given in Display 14.1.

> The implementation for this class is the same as
Display 14.2, except that no definition is given for
t member function printCheck().