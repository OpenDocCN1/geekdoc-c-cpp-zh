name and social security number as arguments (line 10); a C++11 default `virtual` destructor (line 11) that the compiler generates; `set` functions that set the first name, last name and social security number (lines 13, 16 and 19, respectively); `get` functions that return the first name, last name and social security number (lines 14, 17 and 20, respectively); pure `virtual` function `earnings` (line 23) and `virtual` function `toString` (line 24).

```
```cpp
// Fig. 12.9: Employee.h
// Employee abstract base class.
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string> // C++ standard string class

class Employee {
public:
    Employee(const std::string&, const std::string&, const std::string&);
    virtual ~Employee() = default; // compiler generates virtual destructor

    void setFirstName(const std::string&); // set first name
    std::string getFirstName() const; // return first name

    void setLastName(const std::string&); // set last name
    std::string getLastName() const; // return last name

    void setSocialSecurityNumber(const std::string&); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN

    // pure virtual function makes Employee an abstract base class
    virtual double earnings() const = 0; // pure virtual
    virtual std::string toString() const; // virtual
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
};

#endif // EMPLOYEE_H
```
```

# Fig. 12.9 *Employee* abstract base class.