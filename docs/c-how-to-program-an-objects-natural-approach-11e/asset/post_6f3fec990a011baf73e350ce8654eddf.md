
- Derived-class member functions are more likely to be written to depend on the base class's data. Derived classes should depend only on non-private base-class member functions. If we were to change the name of a base-class protected data member, we'd need to modify every derived class that references the data directly. Such software is said to be fragile or brittle. A small change in the base class can “break” the derived class. This is known as the fragile base-class problem 16 and is a key reason the C++ Core Guidelines recommend avoiding protected data. 17 You should be able to change a base class without requiring changes in its derived classes.

Using private data members is better for good software engineering. Declaring base-class data members private lets you change the base-class implementation without requiring changes in derived-class implementations. This makes your code easier to maintain, modify and debug.

A derived class can change the state of private base-class data members only through non-private base-class member functions inherited into the derived class. If a derived class could access its base class's private data members, classes inheriting from that derived class could access the data members as well, and the benefits of information hiding would be lost.

### protected Base-Class Member Functions

One use of protected is to define base-class member functions that should not be exposed to client code but should be accessible in derived classes. A use-case is to enable a derived class to override the base-class protected virtual function and call the original base-class version from the derived class's implementation. 18 We used this capability in the next section.

## 20.5 Non-Virtual Interface (NVI) Idiom

The non-virtual interface (NVI) idiom 19,20—first proposed by Herb Sutter (Convener of the ISO C++ standards committee) in his “Virtuality” paper 21—is another way to implement runtime polymorphism using class hierarchies. This idiom focuses on the good software-engineering practice of separating a class's interface from its implementation. In Chapter 10's runtime polymorphism examples, each public virtual function actually served two purposes:

1. it described part of a class’s interface, indicating how client code could interact with an object of that class, and
2. it described part of a class’s implementation, enabling derived classes to customize behavior (an implementation detail) by overriding the virtual function.

So each public virtual function serves as both part of the class’s interface and its implementation.

For that reason, Sutter says each function should serve only one of these two purposes. Interestingly, a derived class can override its base class’s **private virtual functions**. So, he recommends the following approach to implementing member functions in a class hierarchy:

- **Make each virtual function private**, so it is an implementation detail, not part of the class’s public interface. Doing so ensures that its only purpose is enabling derived classes to customize the base-class behavior by overriding the virtual function. You can make a virtual function protected if each derived class needs to call the base-class virtual function as part of its overridden function definition.
- **Use a public non-virtual function in the base class to invoke that virtual function.** That public non-virtual function will be inherited by all the derived classes and cannot be overridden, so it serves only one purpose—a function the client code calls to perform a task. When the public non-virtual function is called on a derived class object, internally it will call the derived class’s overridden version of the base-class virtual function.

### Refactoring Class Employee for the NVI Idiom

Per Sutter’s guidelines, let’s refactor our Employee class (Figs. 10.11–10.12). Most of the code is identical, so we focus on the following key changes in Fig. 20.14:

- Employee’s public earnings (line 15) and toString (line 16) member functions are no longer declared virtual, and, as you’ll see, earnings will have an implementation. Functions earnings and toString each now serve one purpose—to allow client code to get an Employee’s earnings and string representation, respectively. Their original second purpose—**customization points for derived classes**—will now be implemented via new member functions.
- We added the **protected virtual function getString (line 18) as a customization point for derived classes.** This function is called by the non-virtual toString function. A base class’s **protected members are accessible to its derived classes.** As you’ll see, our derived classes’ getString functions will override and call class Employee’s getString.
- We added the **private pure virtual function getPay (line 21) as a customization point for derived classes.** This function is called by the non-virtual earnings function. Derived classes override getPay to specify custom earnings calculations.

```cpp
// Fig. 20.14: Employee.h
// Employee abstract base class.
#pragma once // prevent multiple inclusions of header
#include <string>
#include <string_view>

class Employee {
public:
    Employee(std::string_view name);
    virtual ~Employee() = default;

    void setName(std::string_view name);
    std::string getName() const;

    double earnings() const; // not virtual
    std::string toString() const; // not virtual
protected:
    virtual std::string getString() const; // virtual
private:
    std::string m_name;
    virtual double getPay() const = 0; // pure virtual
};
```

**Fig. 20.14** | Employee abstract base class.

Figure 20.15 contains several key changes in class Employee’s member-function implementations:

- Member function `earnings` (line 17) now provides a concrete implementation that returns the result of calling the private pure virtual function `getPay`. Even though `getPay` is not yet implemented, this call is allowed because, at execution time, earnings will be called on an object of a concrete derived class of Employee.
- Member function `toString` (line 20) now returns the result of calling the protected virtual function `getString`.
- We now define the new protected member function `getString` (lines 23–25) to specify an Employee’s default string representation containing an Employee’s name. This function is protected so derived classes can override it and call it to get the base-class part of the derived-class string representations.

```cpp
// Fig. 20.15: Employee.cpp
// Abstract-base-class Employee member-function definitions.
// Note: No definitions are given for pure virtual functions.
#include <format>
#include "Employee.h" // Employee class definition

// constructor
Employee::Employee(std::string_view name) : m_name{name} {} // empty body
```

**Fig. 20.15** | Abstract-base-class Employee member-function definitions. (Part 1 of 2.)

```cpp
// set name
void Employee::setName(std::string_view name) {m_name = name;}

// get name
std::string Employee::getName() const {return m_name;}

// public non-virtual function; returns Employee's earnings
double Employee::earnings() const {return getPay();}

// public non-virtual function; returns Employee's string representation
std::string Employee::toString() const {return getString();}

// protected virtual function that derived classes can override and call
std::string Employee::getString() const {
    return std::format("name {}", getName());
}
```

**Fig. 20.15** | Abstract-base-class `Employee` member-function definitions. (Part 2 of 2.)

### Updated Class SalariedEmployee

Our restructured `SalariedEmployee` class (Figs. 20.16–20.17) has several key changes:

- The class’s header (Fig. 20.16) no longer contains prototypes for the `earnings` and `toString` member functions. These **public non-virtual** base-class functions are now inherited from `Employee`.
- The class’s private section now declares overrides for the base class’s private pure virtual function `getPay` and protected virtual function `getString` (Fig. 20.16, lines 19–20). Function `getString` is private in `SalariedEmployee` because this class is final, so no other classes can derive from it.
- The class’s member-function implementations (Fig. 20.17) now include overridden function `getPay` (line 27) to return the salary and overridden function `getString` (lines 30–33) to get a `SalariedEmployee`’s string representation. Note that a `SalariedEmployee`’s `getString` calls `Employee`’s protected `getString` to get part of the string representation.

```cpp
// Fig. 20.16: SalariedEmployee.h
// SalariedEmployee class derived from Employee.
#pragma once
#include <string> // C++ standard string class
#include <string_view>
#include "Employee.h" // Employee class definition

class SalariedEmployee final : public Employee {
public:
    SalariedEmployee(std::string_view name, double salary);
    virtual ~SalariedEmployee() = default; // virtual destructor

    void setSalary(double salary);
    double getSalary() const;
```

**Fig. 20.16** | `SalariedEmployee` class derived from `Employee`. (Part 1 of 2.)
