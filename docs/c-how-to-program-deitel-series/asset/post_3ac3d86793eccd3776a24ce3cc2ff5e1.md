
## Error-Prevention Tip 12.1

![](img/b42ba5cd262b1358d16610173f975e4d_563_0.png)

Apply C++'s override keyword to every overridden function in a derived-class. This forces the compiler to check whether the base class has a member function with the same name and parameter list (i.e., the same signature). If not, the compiler generates an error.

Now, if we aim a base-class CommissionEmployee pointer at a derived-class BasePlusCommissionEmployee object, and the program uses that pointer to call either function earnings or print, the BasePlusCommissionEmployee object's corresponding function will be invoked. There were no changes to the member-function implementations of classes CommissionEmployee and BasePlusCommissionEmployee, so we reuse the versions of Figs. 11.14 and 11.15.

```cpp
// Fig. 12.4: CommissionEmployee.h
// CommissionEmployee class header declares earnings and print as virtual.
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ standard string class

class CommissionEmployee
{
public:
    CommissionEmployee( const std::string &, const std::string &,
        const std::string &, double = 0.0, double = 0.0 );

    void setFirstName( const std::string & ); // set first name
    std::string getFirstName() const; // return first name

    void setLastName( const std::string & ); // set last name
    std::string getLastName() const; // return last name

    void setSocialSecurityNumber( const std::string & ); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN

    void setGrossSales( double ); // set gross sales amount
    double getGrossSales() const; // return gross sales amount

    void setCommissionRate( double ); // set commission rate
    double getCommissionRate() const; // return commission rate

    virtual double earnings() const; // calculate earnings
    virtual void print() const; // print object
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales; // gross weekly sales
    double commissionRate; // commission percentage
}; // end class CommissionEmployee

#endif
```

**Fig. 12.4** | CommissionEmployee class header declares earnings and print as virtual.

```cpp
// aim base-class pointer at derived-class object and print
commissionEmployeePtr = &basePlusCommissionEmployee;
cout << "\nCalling virtual function print with base-class pointer"
     << "\nto derived-class object invokes derived-class "
     << "print function:\n\n";

// polymorphism; invokes BasePlusCommissionEmployee's print;
// base-class pointer to derived-class object
commissionEmployeePtr->print();
cout << endl;
} // end main
```

```
Invoking print function on base-class and derived-class
objects with static binding

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Invoking print function on base-class and derived-class
objects with dynamic binding

Calling virtual function print with base-class pointer
to base-class object invokes base-class print function:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

Calling virtual function print with derived-class pointer
to derived-class object invokes derived-class print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Calling virtual function print with base-class pointer
to derived-class object invokes derived-class print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Note that the base salary is now displayed
```

**Fig. 12.6** | Demonstrating polymorphism by invoking a derived-class virtual function via a base-class pointer to a derived-class object. (Part 2 of 2.)

and ThreeDimensionalShape. The next level of the hierarchy defines concrete classes for two-dimensional shapes (namely, Circle, Square and Triangle) and for three-dimensional shapes (namely, Sphere, Cube and Tetrahedron).

## Pure Virtual Functions

A class is made abstract by declaring one or more of its virtual functions to be “pure.” A pure virtual function is specified by placing “= 0” in its declaration, as in

```cpp
virtual void draw() const = 0; // pure virtual function
```

The “= 0” is a pure specifier. Pure virtual functions typically do not provide implementations, though they can. Each concrete derived class must override all base-class pure virtual functions with concrete implementations of those functions; otherwise, the derived class is also abstract. The difference between a virtual function and a pure virtual function is that a virtual function has an implementation and gives the derived class the option of overriding the function; by contrast, a pure virtual function does not have an implementation and requires the derived class to override the function for that derived class to be concrete; otherwise the derived class remains abstract.

Pure virtual functions are used when it does not make sense for the base class to have an implementation of a function, but you want all concrete derived classes to implement the function. Returning to our earlier example of space objects, it does not make sense for the base class SpaceObject to have an implementation for function draw (as there is no way to draw a generic space object without having more information about what type of space object is being drawn). An example of a function that would be defined as virtual (and not pure virtual) would be one that returns a name for the object. We can name a generic SpaceObject (for instance, as “space object”), so a default implementation for this function can be provided, and the function does not need to be pure virtual. The function is still declared virtual, however, because it’s expected that derived classes will override this function to provide more specific names for the derived-class objects.

> **Software Engineering Observation 12.9**
> 
> An abstract class defines a common public interface for the various classes in a class hierarchy. An abstract class contains one or more pure virtual functions that concrete derived classes must override.

> **Common Programming Error 12.2**
> 
> Failure to override a pure virtual function in a derived class makes that class abstract. Attempting to instantiate an object of an abstract class causes a compilation error.

> **Software Engineering Observation 12.10**
> 
> An abstract class has at least one pure virtual function. An abstract class also can have data members and concrete functions (including constructors and destructors), which are subject to the normal rules of inheritance by derived classes.

Although we cannot instantiate objects of an abstract base class, we can use the abstract base class to declare pointers and references that can refer to objects of any concrete classes

![](img/b42ba5cd262b1358d16610173f975e4d_571_0.png)

**Fig. 12.7**  Employee hierarchy UML class diagram.

> **Software Engineering Observation 12.11**
> 
> A derived class can inherit interface and/or implementation from a base class. Hierarchies designed for implementation inheritance tend to have their functionality high in the hierarchy—a rich and very general class inherits one or more members/functions that were defined in a base class, and the derived class uses the base-class definitions. Hierarchies designed for interface inheritance tend to have their functionality lower in the hierarchy—a base class specifies one or more functions that should be defined for each class in the hierarchy (i.e., they have the same prototype), but the individual derived classes provide their own implementations of the function(s).

The following sections implement the Employee class hierarchy. The first five each implement one of the abstract or concrete classes. The last section implements a test program that builds objects of all these classes and processes the objects polymorphically.

### 12.6.1 Creating Abstract Base Class Employee

Class Employee (Figs. 12.9–12.10, discussed in further detail shortly) provides functions earnings and print, in addition to various get and set functions that manipulate Employee’s data members. An earnings function certainly applies generally to all employees, but each earnings calculation depends on the employee’s class. So we declare earnings as pure virtual in base class Employee because a *default implementation does not make sense* for that function—there is not enough information to determine what amount earnings should return. Each derived class *overrides* earnings with an appropriate implementation. To calculate an employee’s earnings, the program assigns the address of an employee’s object to a base class Employee *pointer*, then invokes the earnings function on that object. We maintain a vector of Employee pointers, each of which points to an Employee object. *Of course, there cannot be Employee objects, because Employee is an abstract class—because of inheritance, however, all objects of all concrete derived classes of Employee may nevertheless be thought of as Employee objects.* The program iterates through the vector and calls function earnings for each Employee object. C++ processes these function calls *polymorphically*. Including earnings as a pure virtual function in Employee *forces* every direct derived class of Employee that wishes to be a *concrete class* to override earnings.

Function print in class Employee displays the first name, last name and social security number of the employee. As we’ll see, each derived class of Employee overrides function
