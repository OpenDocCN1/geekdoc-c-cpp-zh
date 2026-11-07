of the data member. For example, if our preceding variable `martianCount` is public, it can be accessed with the expression `Martian::martianCount` when there are no Martian objects. (Of course, using public data is discouraged.)

To access a private or protected static class member when no objects of the class exist, provide a public **static member function** and call the function by prefixing its name with the class name and scope resolution operator. A static member function is a service of the *class*, not of a specific object of the class.

> **Software Engineering Observation 10.10**
> 
> A class’s static data members and static member functions exist and can be used even if no objects of that class have been instantiated.

# Demonstrating *static* Data Members

The program of Figs. 10.18–10.20 demonstrates a private static data member called count (Fig. 10.18, line 25) and a public static member function called getCount (Fig. 10.18, line 19). In Fig. 10.19, line 8 defines and initializes the data member count to zero at global namespace scope and lines 12–15 define static member function getCount. Notice that neither line 8 nor line 12 includes keyword static, yet both lines refer to static class members. When static is applied to an item at global namespace scope, that item becomes known only in that file. The static class members need to be available to any client code that uses the class, so we declare the static only in the .h file. Data member count maintains a count of the number of objects of class Employee that have been instantiated. When objects of class Employee exist, member count can be referenced through any member function of an Employee object—in Fig. 10.19, count is referenced by both line 22 in the constructor and line 32 in the destructor.

> **Common Programming Error 10.8**
> 
> It’s a compilation error to include keyword `static` in the definition of a static data member at global namespace scope.

```
```cpp
// Fig. 10.18: Employee.h
// Employee class definition with a static data member to
// track the number of Employee objects in memory
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>
using namespace std;

class Employee
{
public:
   Employee( const string &, const string & ); // constructor
   ~Employee(); // destructor
   string getFirstName() const; // return first name
   string getLastName() const; // return last name
```
```

**Fig. 10.18** — *Employee class definition with a static data member to track the number of Employee objects in memory. (Part 1 of 2.)*