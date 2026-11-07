# **Program 11.11**  File employee.h

```
```cpp
/************************************************************
 * The interface file to define the Student class           *
 ************************************************************/
#ifndef EMPLOYEE_H
#define EMPLOYEE_H
#include "person.h"

// Definition of the Employee class
class Employee : public Person
{
private:
    string name;
    double salary;
public:
    Employee (string name, double salary);
    ~Employee ();
    void print () const;
};
#endif
```
```

# **Program 11.12**  File employee.cpp

```
```cpp
/************************************************************
 * The implementation file for the Employee class           *
 ************************************************************/
#include "employee.h"

// Constructor for Employee class
Employee::Employee (string nm, double sa)
:Person (nm), salary (sa)
{
}
// Destructor for Employee class
Employee::~Employee()
{
}
// Definition of print member function
void Employee::print () const
{
    Person::print();
    cout << "Salary: " << salary << endl;
}
```
```