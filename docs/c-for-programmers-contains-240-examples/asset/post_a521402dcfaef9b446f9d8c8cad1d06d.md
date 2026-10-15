
## 13.8 Case Study: Payroll System Using Polymorphism and Runtime Type Information with Downcasting, dynamic_cast, typeid and type_info

Recall from the problem statement at the beginning of Section 13.6 that, for the current pay period, our fictitious company has decided to reward BasePlusCommissionEmployees by adding 10 percent to their base salaries. When processing Employee objects polymorphically in Section 13.6.6, we did not need to worry about the “specifics.” Now, however, to adjust the base salaries of BasePlusCommissionEmployees, we have to determine the specific type of each Employee object at execution time, then act appropriately. This section demonstrates the powerful capabilities of runtime type information (RTTI) and dynamic casting, which enable a program to determine the type of an object at execution time and act on that object accordingly.

> [Note: Some compilers require that RTTI be enabled before it can be used in a program. Consult your compiler’s documentation to determine whether your compiler has similar requirements. In Visual C++ 2005, this option is enabled by default.]

Figure 13.25 uses the Employee hierarchy developed in Section 13.6 and increases by 10 percent the base salary of each BasePlusCommissionEmployee. Line 31 declares four-element vector employees that stores pointers to Employee objects. Lines 34-41 populate the vector with the addresses of dynamically allocated objects of classes SalariedEmployee (Figs. 13.15-13.16), HourlyEmployee (Figs. 13.17-13.18), CommissionEmployee (Figs. 13.19-13.20) and BasePlusCommissionEmployee (Figs. 13.21-13.22).

```
1 // Fig. 13.25: fig13_25.cpp
2 // Demonstrating downcasting and runtime type information.
3 // NOTE: You may need to enable RTTI on your compiler
4 // before you can execute this application.
5 #include <iostream>
6 using std::cout;
7 using std::endl;
8 using std::fixed;
9 
10 #include <iomanip>
11 using std::setprecision;
12 
13 #include <vector>
14 using std::vector;
15 
16 #include <typeinfo>
17 
18 // include definitions of classes in Employee hierarchy
19 #include "Employee.h"
20 #include "SalariedEmployee.h"
21 #include "HourlyEmployee.h"
22 #include "CommissionEmployee.h"
23 #include "BasePlusCommissionEmployee.h"
24 
25 int main()
26 {
```

Line 65 invokes member function earnings on the object to which employees[ i ] points. Recall that earnings is declared virtual in the base class, so the program invokes the derived-class object’s earnings function—another example of dynamic binding.

Lines 69–76 display each employee’s object type and uses the delete operator to deallocate the dynamic memory to which each vector element points. Operator typeid (line 73) returns a reference to an object of class type_info that contains the information about the type of its operand, including the name of that type. When invoked, type_info member function name (line 73) returns a pointer-based string that contains the type name (e.g., "class BasePlusCommissionEmployee") of the argument passed to typeid. To use typeid, the program must include header file <typeinfo> (line 16).

### Portability Tip 13.1

> The string returned by type_info member function name may vary by compiler.

Note that we avoid several compilation errors in this example by downcasting an Employee pointer to a BasePlusCommissionEmployee pointer (lines 50–52). If we remove the dynamic_cast from line 51 and attempt to assign the current Employee pointer directly to BasePlusCommissionEmployee pointer derivedPtr, we’ll receive a compilation error. C++ does not allow a program to assign a base-class pointer to a derived-class pointer because the is-a relationship does not apply—a CommissionEmployee is not a BasePlusCommissionEmployee. The is-a relationship applies only between the derived class and its base classes, not vice versa.

Similarly, if lines 58, 60 and 62 used the current base-class pointer from employees, rather than derived-class pointer derivedPtr, to invoke derived-class-only functions getBaseSalary and setBaseSalary, we would receive a compilation error at each of these lines. As you learned in Section 13.3.3, attempting to invoke derived-class-only functions through a base-class pointer is not allowed. Although lines 58, 60 and 62 execute only if commissionPtr is not 0 (i.e., if the cast can be performed), we cannot attempt to invoke derived-class BasePlusCommissionEmployee functions getBaseSalary and setBaseSalary on the base-class Employee pointer. Recall that, using a base class Employee pointer, we can invoke only functions found in base class Employee—earnings, print and Employee’s get and set functions.

## 13.9 Virtual Destructors

A problem can occur when using polymorphism to process dynamically allocated objects of a class hierarchy. So far you have seen nonvirtual destructors—destructors that are not declared with keyword virtual. If a derived-class object with a nonvirtual destructor is destroyed explicitly by applying the delete operator to a base-class pointer to the object, the C++ standard specifies that the behavior is undefined.

The simple solution to this problem is to create a virtual destructor (i.e., a destructor that is declared with keyword virtual) in the base class. This makes all derived-class destructors virtual even though they do not have the same name as the base-class destructor. Now, if an object in the hierarchy is destroyed explicitly by applying the delete operator to a base-class pointer, the destructor for the appropriate class is called based on the object to which the base-class pointer points. Remember, when a derived-class object is destroyed, the base-class part of the derived-class object is also destroyed, so it is important for the destructors of both the derived class and base class to execute. The base-class destructor automatically executes after the derived-class destructor.

### Error-Prevention Tip 13.2

> If a class has virtual functions, provide a virtual destructor, even if one is not required for the class. This ensures that a custom derived-class destructor (if there is one) will be invoked when a derived-class object is deleted via a base class pointer.

### Common Programming Error 13.5

> Constructors cannot be virtual. Declaring a constructor virtual is a compilation error.

## 13.10 (Optional) Software Engineering Case Study: Incorporating Inheritance into the ATM System

We now revisit our ATM system design to see how it might benefit from inheritance. To apply inheritance, we first look for commonality among classes in the system. We create an inheritance hierarchy to model similar (yet not identical) classes in a more efficient and elegant manner that enables us to process objects of these classes polymorphically. We then modify our class diagram to incorporate the new inheritance relationships. Finally, we demonstrate how our updated design is translated into C++ header files.

In Section 3.11, we encountered the problem of representing a financial transaction in the system. Rather than create one class to represent all transaction types, we decided to create three individual transaction classes—BalanceInquiry, Withdrawal and Deposit—to represent the transactions that the ATM system can perform. Figure 13.26 shows the attributes and operations of these classes. Note that they have one attribute (accountNumber) and one operation (execute) in common. Each class requires attribute accountNumber to specify the account to which the transaction applies. Each class contains operation execute, which the ATM invokes to perform the transaction. Clearly, BalanceInquiry, Withdrawal and Deposit represent types of transactions. Figure 13.26 reveals commonality among the transaction classes, so using inheritance to factor out the common features seems appropriate for designing these classes. We place the common functionality in base class Transaction and derive classes BalanceInquiry, Withdrawal and Deposit from Transaction (Fig. 13.27).

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_614_0.png)

Fig. 13.26 | Attributes and operations of classes BalanceInquiry, Withdrawal and Deposit.
