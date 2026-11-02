
```cpp
40 // print BasePlusCommissionEmployee object
41 void BasePlusCommissionEmployee::print() const
42 {
43    // derived class cannot access the base class's private data
44    cout << "base-salaried commission employee: " << firstName << ' '
45         << lastName << "\nsocial security number: " << socialSecurityNumber
46         << "\ngross sales: " << grossSales
47         << "\ncommission rate: " << commissionRate
48         << "\nbase salary: " << baseSalary;
49 } // end function print
```

*Compilation Errors from the LLVM Compiler in Xcode*

```text
BasePlusCommissionEmployee.cpp:37:26:
    'commissionRate' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:37:49:
    'grossSales' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:44:53:
    'firstName' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:45:10:
    'lastName' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:45:54:
    'socialSecurityNumber' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:46:31:
    'grossSales' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:47:35:
    'commissionRate' is a private member of 'CommissionEmployee'
```

**Fig. 19.11 |** BasePlusCommissionEmployee implementation file. Private base-class data cannot be accessed from derived class. (Part 2 of 2.)

Figure 19.11 shows BasePlusCommissionEmployee's member-function implementations. The constructor (lines 9–16) introduces base-class initializer syntax (line 13), which uses a member initializer to pass arguments to the base class (CommissionEmployee) constructor. C++ requires that a derived-class constructor call its base-class constructor to initialize the base-class data members that are inherited into the derived class. Line 13 does this by explicitly invoking the CommissionEmployee constructor by name, passing the constructor's parameters first, last, ssn, sales and rate as arguments to initialize the base-class data members firstName, lastName, socialSecurityNumber, grossSales and commissionRate, respectively. If BasePlusCommissionEmployee's constructor did not invoke class CommissionEmployee's constructor explicitly, C++ would attempt to invoke class CommissionEmployee's default constructor implicitly—but the class does not have such a constructor, so the compiler would issue an error. Recall from Chapter 16 that the compiler provides a default constructor with no parameters in any class that does not explicitly include a constructor. However, CommissionEmployee does explicitly include a constructor, so a default constructor is not provided.

### **Common Programming Error 19.1**

When a derived-class constructor calls a base-class constructor, the arguments passed to the base-class constructor must be consistent with the number and types of parameters specified in one of the base-class constructors; otherwise, a compilation error occurs.

### Performance Tip 19.1

In a derived-class constructor, invoking base-class constructors and initializing member objects explicitly in the member initializer list prevents duplicate initialization in which a default constructor is called, then data members are modified again in the derived-class constructor's body.

### Compilation Errors from Accessing Base-Class private Members

The compiler generates errors for line 37 of Fig. 19.11 because base class CommissionEmployee's data members commissionRate and grossSales are private—derived class BasePlusCommissionEmployee's member functions are not allowed to access base class CommissionEmployee's private data. The compiler issues additional errors in lines 44–47 of BasePlusCommissionEmployee's print member function for the same reason. As you can see, C++ rigidly enforces restrictions on accessing private data members, so that even a derived class (which is intimately related to its base class) cannot access the base class's private data.

### Preventing the Errors in BasePlusCommissionEmployee

We purposely included the erroneous code in Fig. 19.11 to emphasize that a derived class's member functions cannot access its base class's private data. The errors in BasePlusCommissionEmployee could have been prevented by using the get member functions inherited from class CommissionEmployee. For example, line 37 could have invoked getCommissionRate and getGrossSales to access CommissionEmployee's private data members commissionRate and grossSales, respectively. Similarly, lines 44–47 could have used appropriate get member functions to retrieve the values of the base class's data members. In the next example, we show how using protected data also allows us to avoid the errors encountered in this example.

### Including the Base-Class Header in the Derived-Class Header with #include

Notice that we #include the base class's header in the derived class's header (line 8 of Fig. 19.10). This is necessary for three reasons. First, for the derived class to use the base class's name in line 10, we must tell the compiler that the base class exists—the class definition in CommissionEmployee.h does exactly that.

The second reason is that the compiler uses a class definition to determine the size of an object of that class (as we discussed in Section 16.6). A client program that creates an object of a class #includes the class definition to enable the compiler to reserve the proper amount of memory for the object. When using inheritance, a derived-class object's size depends on the data members declared explicitly in its class definition and the data members inherited from its direct and indirect base classes. Including the base class's definition in line 8 allows the compiler to determine the memory requirements for the base class's data members that become part of a derived-class object and thus contribute to the total size of the derived-class object.

The last reason for line 8 is to allow the compiler to determine whether the derived class uses the base class's inherited members properly. For example, in the program of Figs. 19.10–19.11, the compiler uses the base-class header to determine that the data members being accessed by the derived class are private in the base class. Since these are inaccessible to the derived class, the compiler generates errors. The compiler also uses the base class's function prototypes to validate function calls made by the derived class to the inherited base-class functions.

## Linking Process in an Inheritance Hierarchy

In Section 16.7, we discussed the linking process for creating an executable GradeBook application. In that example, you saw that the client’s object code was linked with the object code for class GradeBook, as well as the object code for any C++ Standard Library classes used in either the client code or in class GradeBook.

The linking process is similar for a program that uses classes in an inheritance hierarchy. The process requires the object code for all classes used in the program and the object code for the direct and indirect base classes of any derived classes used by the program. Suppose a client wants to create an application that uses class BasePlusCommissionEmployee, which is a derived class of CommissionEmployee (we’ll see an example of this in Section 19.3.4). When compiling the client application, the client’s object code must be linked with the object code for classes BasePlusCommissionEmployee and CommissionEmployee, because BasePlusCommissionEmployee inherits member functions from its base class CommissionEmployee. The code is also linked with the object code for any C++ Standard Library classes used in class CommissionEmployee, class BasePlusCommissionEmployee or the client code. This provides the program with access to the implementations of all of the functionality that the program may use.

## 19.3.4 CommissionEmployee–BasePlusCommissionEmployee Inheritance Hierarchy Using protected Data

Chapter 16 introduced access specifiers public and private. A base class’s public members are accessible within its body and anywhere that the program has a handle (i.e., a name, reference or pointer) to an object of that class or one of its derived classes. A base class’s private members are accessible only within its body and to the friends of that base class. In this section, we introduce the access specifier protected.

Using protected access offers an intermediate level of protection between public and private access. To enable class BasePlusCommissionEmployee to directly access CommissionEmployee data members firstName, lastName, socialSecurityNumber, grossSales and commissionRate, we can declare those members as protected in the base class. A base class’s protected members can be accessed within the body of that base class, by members and friends of that base class, and by members and friends of any classes derived from that base class.

### Defining Base Class CommissionEmployee with protected Data

Class CommissionEmployee (Fig. 19.12) now declares data members firstName, lastName, socialSecurityNumber, grossSales and commissionRate as protected (lines 31–36) rather than private. The member-function implementations are identical to those in Fig. 19.5, so CommissionEmployee.cpp is not shown here.

```cpp
// Fig. 19.12: CommissionEmployee.h
// CommissionEmployee class definition with protected data.
#ifndef COMMISSION_H
#define COMMISSION_H
```

**Fig. 19.12** | CommissionEmployee class definition that declares protected data to allow access by derived classes. (Part 1 of 2.)
