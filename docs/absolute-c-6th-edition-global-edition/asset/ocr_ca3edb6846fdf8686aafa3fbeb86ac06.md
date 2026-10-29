setting and changing names and Social Security numbers will be the same for salaried and hourly employees.

Within C++ you can define a class called Employee that includes all employees, whether salaried or hourly and then use this class to define classes for hourly employees and salaried employees.

The class Employee will also contain member functions that manipulate the data fields of the class Employee. Displays 14.1 and 14.2 show one possible definition for the class Employee.

# Display 14.1 Interface for the Base Class Employee

```
1 //This is the header file employee.h.
2 //This is the interface for the class Employee.
3 //This is primarily intended to be used as a base class to derive
4 //classes for different kinds of employees.
5 #ifndef EMPLOYEE_H
6 #define EMPLOYEE_H
7 
8 #include <string>
9 using std::string;
10 
11 namespace SavitchEmployees
12 {
13 
14 class Employee
15 {
16 public:
17 Employee();
18 Employee(const string& theName, const string& theSsn);
19 string getName() const;
20 string getSsn() const;
21 double getNetPay() const;
22 void setName(const string& newName);
23 void setSsn(const string& newSsn);
24 void setNetPay(double newNetPay);
25 void printCheck() const;
26 private:
27 string name;
28 string ssn;
29 double netPay;
30 };
31 
32 };//SavitchEmployees
33 
34 #endif //EMPLOYEE_H
```