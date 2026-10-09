
# Compilation Errors from the Clang/LLVM Compiler in Xcode 7.2

| `BasePlusCommissionEmployee.cpp:34:25:` | `'commissionRate' is a private member of 'CommissionEmployee'` |
| `BasePlusCommissionEmployee.cpp:34:42:` | `'grossSales' is a private member of 'CommissionEmployee'` |
| `BasePlusCommissionEmployee.cpp:42:55:` | `'firstName' is a private member of 'CommissionEmployee'` |
| `BasePlusCommissionEmployee.cpp:43:10:` | `'lastName' is a private member of 'CommissionEmployee'` |
| `BasePlusCommissionEmployee.cpp:43:54:` | `'socialSecurityNumber' is a private member of 'CommissionEmployee'` |
| `BasePlusCommissionEmployee.cpp:44:31:` | `'grossSales' is a private member of 'CommissionEmployee'` |
| `BasePlusCommissionEmployee.cpp:45:33:` | `'commissionRate' is a private member of 'CommissionEmployee'` |

> Fig. 11.11 | `BasePlusCommissionEmployee` implementation file: private base-class cannot be accessed from derived class. (Part 2 of 2).

`constructor`. C++ requires that a derived-class constructor calls its base-class constructor to initialize the base-class data members that are inherited by derived class. Line 14 does this by explicitly invoking the `CommissionEmployee` constructor by name, passing the constructor's parameters `first`, `last`, `ssn`, `sales` and `rate` as arguments to initialize the base-

## Chapter II Object-Oriented Programming: Inheritance

class data members `firstName`, `lastName`, `socialSecurityNumber`, `grossSales` and `commission-rate`, respectively. The compiler would issue an error if `BasePlusCommissionEmployee`'s constructor did not invoke class `CommissionEmployee`'s constructor explicitly—in this case, C++ attempts to invoke `CommissionEmployee`'s default constructor implicitly, but the class does not have such a constructor. Recall from Chapter 3 that the compiler provides a default constructor with no parameters in any class that not explicitly include a constructor. However, `CommissionEmployee` does explicitly include a constructor, so a default constructor is not provided.

![](img/06ca63376760c659af4aa0e9c282068d_554_0.png)

### Common Programming Error II.1

When a derived-class constructor calls a base-class, the arguments passed to the base-class constructor must be consistent with the number and types of parameters specified in one of the base-class constructors; otherwise, a compilation error occurs.

![](img/06ca63376760c659af4aa0e9c282068d_554_1.png)

### Performance Tip II.1

In a derived-class constructor, invoking base-class constructors and initializing member objects explicitly in the member initializer list prevents duplicate initialization if a default constructor is called, then data members are modified again in the derived-class constructor's body.

### Compilation Errors from Base-Class Private Members

The compiler generates errors for line 35 of Fig. II.11 because base-class `CommissionEmployee`'s data members `commissionRate` and `grossSales` are private—derived-class `BasePlusCommissionEmployee`'s member functions are not allowed to access base `CommissionEmployee`'s private data. The compiler issues additional errors in lines 44–47 of `BasePlusCommissionEmployee`'s `toString` member function for the same reason. As you can see, C++ rigidly enforces restrictions on accessing private data members, that even a derived-class (which is intimately related to its base-class) cannot access the base-class private data.

### Preventing the Errors in BasePlusCommissionEmployee

We purposely included the erroneous code in Fig. II.11 to emphasize that a derived-class's member cannot access its base-class private data. The errors in `BasePlusCommissionEmployee` could have been prevented by using the `get` member functions inherited from class `CommissionEmployee`. For example, line 35 could have invoked `commissionRate` and `grossSales` to access `CommissionEmployee`'s private data members respectively. Similarly, lines 44–47 could have used appropriate `get` functions to retrieve the values of the base-class data members. In the next example, we show how using protected data allows us to avoid the errors encountered in this example.

### Including the Base-Class Header in the Derived-Class Header with `#include`

Notice that we include the base-class header in the derived-class header (line 8 of II.10). This is necessary for three reasons. First, for the derived class to use the base-class name in line 10, we must tell the compiler that the base class exists—the class definition in `CommissionEmployee.h` does exactly that.

## 11.3 Relationship between Base and Derived Classes 555

The second reason is that the compiler uses a class definition to determine the size of an object of that class (as discussed in Section 9.3). A client program that creates an object of class includes the class definition to enable the compiler to reserve the proper amount of memory for the object. When using inheritance, a derived-class size depends on the data members declared explicitly in its class and the data members inherited from its direct and indirect base classes. Including the base class definition in line 8 of Fig. 10 allows the compiler to determine the memory requirements for the base class's data members that become part of a derived-class object and contribute to its total size.

The last reason for line 8 is to allow the compiler to determine whether the derived class uses the base class's inherited members properly. For example, in the program of Fig. 10-11, the compiler uses the base-class header to determine that the members being accessed by the derived class are private in the base class. Since these are inaccessible to the derived class, the compiler generates errors. The compiler also uses the base class's function prototypes to validate function calls by the derived class to the inherited-base-class functions.

### Linking Process in an Inheritance Hierarchy

In Section 9.3, we discussed the linking process for creating an executable application. In example, you saw that the client's object code was linked with the object code for `time`, as well as the object code for any C++ Standard Library classes either in the client code or in `time`.
The linking process is similar for a program that uses classes in an inheritance hierarchy. The process requires the object code for all classes used in the program and the object code for the direct and indirect base classes of any derived classes. Suppose a client wants to create an application that uses classes derived `BasePlusEmployee`(we'll see an example of this in Section 11.3.4). When compiling the code, the client's object code must be linked with the object code for `BasePlusEmployee` and `CommissionEmployee`, because `BasePlusEmployee` inherits members from its base-class `CommissionEmployee`. The code is also linked with the object code for any C++ Standard Library classes used in `CommissionEmployee`, `BasePlusCommissionEmployee` or the client code. This provides the program with access to the implementations of all the functionality that the program may use.

### 11.3.4 CommissionEmployee—BasePlusEmployee Inheritance Using Protected Data

Chapter 3 introduced access specifiers `public` and `private`. A base class's public members are accessible within its body and anywhere the program has a handle (i.e., a name, reference or pointer) to an object of that class or one of its derived classes, including in classes. A base class's private members are accessible only within its own body and to the friends of that class. In this section, we introduce the access specifier `protected`.

Using protected access offers an intermediate level of protection between public and private access. To enable class `BasePlusEmployee` to directly access `CommissionEmployee` data members `firstName`, `lastName`, `socialSecurityNumber`, `grossSales`

# 第 II 章 面向对象编程：继承

`commissionRate`，我们将这些成员声明为基类中的 `protected`。基类的 `protected` 成员可以在该基类的主体内、该基类的成员和友元中，以及从该类派生的任何类的成员和友元中访问。

使用 `protected` 数据定义基类 `CommissionEmployee`
`CommissionEmployee`（图 11.12）现在将数据成员 `firstName`、`lastName`、`socialSecurityNumber`、`grossSales` 和 `commissionRate` 声明为 `protected`（第 30–35 行），而不是 `private`。成员函数的实现与图 11.5 中的相同，因此此处不显示 `CommissionEmployee.cpp`。
