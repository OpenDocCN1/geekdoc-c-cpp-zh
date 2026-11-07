A derived class can inherit interface and/or implementation from a base class. **Hierarchies designed for interface inheritance tend to have concrete definitions of their functionality lower in the hierarchy.** A base class declares one or more functions that should be defined by every derived class, but the individual derived classes provide the implementations of the function(s).

The following subsections implement the Employee class hierarchy. The first three each define one of the abstract or concrete classes. The last contains a test program that builds concrete-class objects and processes them with runtime polymorphism.

# 10.9.1 Creating Abstract Base Class Employee

Class Employee (Figs. 10.11–10.12, discussed in further detail shortly) provides functions `earnings` and `toString`, and `get` and `set` functions that manipulate Employee’s `m_name` data member. An earnings function generally applies to all Employees, but each calculation depends on the kind of Employee. So we declare all earnings as pure virtual in base class Employee because a default implementation does not make sense for that function. There’s not enough information to determine what amount earnings should return.

Each derived class overrides `earnings` with an appropriate implementation. To calculate an employee’s earnings, the program assigns an employee object’s address to a base-class Employee pointer, then invokes the object’s `earnings` function.

The test program contains a vector of Employee pointers. Each points to an object that **is** an Employee—specifically, any object of a concrete derived class of Employee. The program iterates through the vector and polymorphically calls each Employee’s `earnings` function. **Making earnings a pure virtual function in Employee forces every derived class of Employee that wishes to be a concrete class to override earnings.**

Employee’s `toString` function returns a string containing the Employee’s name. Each class derived from Employee will override `toString` to return the name followed by the rest of the Employee’s information. Each derived class’s `toString` could also call `earnings`, even though `earnings` is a pure virtual function in Employee. Each concrete class is guaranteed to have an earnings implementation. Even class Employee’s `toString` function can call earnings. When you call `toString` through an Employee pointer or reference at runtime, you always call it on a concrete derived-class object.

The following diagram shows the hierarchy’s three classes down the left and functions `earnings` and `toString` across the top. For each class, the diagram shows the desired return value of each function.

| Class | earnings | toString |
|---|---|---|
| Employee | pure virtual | name: `m_name` |
| Salaried-Employee | `m_salary` | name: `m_name`<br>salary: `m_salary` |
| Commission-Employee | `m_commissionRate * m_grossSales` | name: `m_name`<br>gross sales: `m_grossSales`<br>commission rate: `m_commissionRate` |

*Italic text represents where the values from a particular object are used in the earnings and toString functions. Class Employee specifies “pure virtual” for function earnings*