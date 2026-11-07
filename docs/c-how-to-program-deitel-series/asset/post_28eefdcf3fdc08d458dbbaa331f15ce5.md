
| Base class | Derived classes |
|---|---|
| Student | GraduateStudent, UndergraduateStudent |
| Shape | Circle, Triangle, Rectangle, Sphere, Cube |
| Loan | CarLoan, HomeImprovementLoan, MortgageLoan |
| Employee | Faculty, Staff |
| Account | CheckingAccount, SavingsAccount |

**Fig. 11.1** | *Inheritance examples.*

Because every derived-class object is an object of its base class, and one base class can have many derived classes, the set of objects represented by a base class typically is larger than the set of objects represented by any of its derived classes. For example, the base class Vehicle represents all vehicles, including cars, trucks, boats, airplanes, bicycles and so on. By contrast, derived class Car represents a smaller, more specific subset of all vehicles.

Inheritance relationships form class hierarchies. A base class exists in a hierarchical relationship with its derived classes. Although classes can exist independently, once they’re employed in inheritance relationships, they become affiliated with each other. A class becomes either a base class—supplying members to other classes, a derived class—inheriting its members from other classes, or both.

## CommunityMember Class Hierarchy

Let’s develop a simple inheritance hierarchy with five levels (represented by the UML class diagram in Fig. 11.2). A university community has thousands of CommunityMembers.

These CommunityMembers consist of Employees, Students and alumni (each of class Alumnus). Employees are either Faculty or Staff. Faculty are either Administrators or Teachers. Some Administrators, however, are also Teachers. We've used *multiple inheritance* to form class `AdministratorTeacher`. With *single inheritance*, a class is derived from one base class. With *multiple inheritance*, a derived class inherits simultaneously from two or more (possibly unrelated) base classes. We discuss multiple inheritance in Chapter 23, Other Topics, but multiple inheritance is generally discouraged.

Each arrow in the hierarchy (Fig. 11.2) represents an *is-a* relationship. For example, as we follow the arrows in this class hierarchy, we can state “an Employee is a CommunityMember” and “a Teacher is a Faculty member.” CommunityMember is the *direct base class* of Employee, Student and Alumnus. In addition, CommunityMember is an *indirect base class* of all the other classes in the diagram. An indirect base class is inherited from two or more levels up the class hierarchy.

Starting from the bottom of the diagram you can follow the arrows upwards and apply the *is-a* relationship to the topmost base class. For example, an AdministratorTeacher is an Administrator, is a Faculty member, is an Employee and is a CommunityMember.

![](img/b42ba5cd262b1358d16610173f975e4d_519_0.png)

**Fig. 11.2** | *Inheritance hierarchy for university CommunityMembers.*

## Shape Class Hierarchy

Now consider the Shape inheritance hierarchy in Fig. 11.3. This hierarchy begins with base class Shape. Classes TwoDimensionalShape and ThreeDimensionalShape derive from base class Shape—a Shape is a TwoDimensionalShape or is a ThreeDimensionalShape. The third level of this hierarchy contains *more specific* types of TwoDimensionalShapes and ThreeDimensionalShapes. As in Fig. 11.2, we can follow the arrows from the bottom of the diagram upwards to the topmost base class in this hierarchy to identify several *is-a* relationships. For instance, a Triangle is a TwoDimensionalShape and is a Shape, while a Sphere is a ThreeDimensionalShape and is a Shape.

![](img/b42ba5cd262b1358d16610173f975e4d_520_0.png)

**Fig. 11.3** | *Inheritance hierarchy for Shapes.*

To specify that class TwoDimensionalShape (Fig. 11.3) is derived from (or inherits from) class Shape, class TwoDimensionalShape's definition could begin as follows:

```cpp
class TwoDimensionalShape : public Shape
```

This is an example of *public inheritance*, the most commonly used form. We'll also discuss *private inheritance* and *protected inheritance* (Section 11.5). With all forms of inheritance, private members of a base class are *not* accessible directly from that class's derived classes, but these private base-class members are still inherited (i.e., they're still considered parts of the derived classes). With public inheritance, all other base-class members retain their original member access when they become members of the derived class (e.g., public members of the base class become public members of the derived class, and as we'll soon see, protected members of the base class become protected members of the derived class). Through inherited base-class member functions, the derived class can manipulate private members of the base class (if these inherited member functions provide such functionality in the base class). Note that friend functions are *not inherited*.

Inheritance is *not* appropriate for every class relationship. In Chapter 9, we discussed the *has-a* relationship, in which classes have members that are objects of other classes. Such relationships create classes by *composition* of existing classes. For example, given the classes `Employee`, `BirthDate` and `TelephoneNumber`, it's improper to say that an `Employee` *is a* `BirthDate` or that an `Employee` *is a* `TelephoneNumber`. However, it is appropriate to say that an `Employee` *has a* `BirthDate` and that an `Employee` *has a* `TelephoneNumber`.

It’s possible to treat base-class objects and derived-class objects similarly; their commonalities are expressed in the members of the base class. Objects of all classes derived from a common base class can be treated as objects of that base class (i.e., such objects have an *is-a* relationship with the base class). In Chapter 12, we consider many examples that take advantage of this relationship.

## 11.3 Relationship between Base and Derived Classes

In this section, we use an inheritance hierarchy containing types of employees in a company’s payroll application to discuss the relationship between a base class and a derived class. Commission employees (who will be represented as objects of a base class) are paid a percentage of their sales, while base-salaried commission employees (who will be represented as objects of a derived class) receive a base salary plus a percentage of their sales. We divide our discussion of the relationship between commission employees and base-salaried commission employees into a carefully paced series of five examples.

### 11.3.1 Creating and Using a CommissionEmployee Class

Let’s examine `CommissionEmployee`’s class definition (Figs. 11.4–11.5). The CommissionEmployee header (Fig. 11.4) specifies class `CommissionEmployee`’s public services, which include a constructor (lines 1–12) and member functions appearing (line 29) and print (line 30). Lines 14–27 declare `public` get and set functions that manipulate the class’s data members (declared in lines 32–36)—`firstName`, `lastName`, `socialSecurityNumber`, `grossSales` and `commissionRate`. Member functions `setGrossSales` (defined in lines 57–63 of Fig. 11.5) and `setCommissionRate` (defined in lines 72–78 of Fig. 11.5), for example, validate their arguments before assigning the values to data members `grossSales` and `commissionRate`, respectively.

```cpp
// Fig. 11.4: CommissionEmployee.h
// CommissionEmployee class definition represents a commission employee.
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ standard string class

class CommissionEmployee
{
public:
   CommissionEmployee( const std::string &, const std::string &,
      const std::string &, double = 0.0, double = 0.0 );

   void setFirstName( const std::string & ); // set first name
   std::string getFirstName() const;         // return first name

   void setLastName( const std::string & );  // set last name
   std::string getLastName() const;          // return last name

   void setSocialSecurityNumber( const std::string & ); // set SSN
   std::string getSocialSecurityNumber() const;         // return SSN

   void setGrossSales( double ); // set gross sales amount
   double getGrossSales() const; // return gross sales amount

   void setCommissionRate( double ); // set commission rate (percentage)
   double getCommissionRate() const; // return commission rate

   double earnings() const; // calculate earnings
   void print() const;      // print CommissionEmployee object
private:
   std::string firstName;
   std::string lastName;
   std::string socialSecurityNumber;
   double grossSales;      // gross weekly sales
   double commissionRate;  // commission percentage
}; // end class CommissionEmployee

#endif
```

**Fig. 11.4** | *CommissionEmployee class header.*

```cpp
// Fig. 11.5: CommissionEmployee.cpp
// Class CommissionEmployee member-function definitions.
#include <iostream>
#include <stdexcept>
#include "CommissionEmployee.h" // CommissionEmployee class definition
using namespace std;

// constructor
CommissionEmployee::CommissionEmployee(
   const string &first, const string &last, const string &ssn,
   double sales, double rate )
{
   firstName = first; // should validate
   lastName = last; // should validate
   socialSecurityNumber = ssn; // should validate
   setGrossSales( sales ); // validate and store gross sales
```

**Fig. 11.5** | *Implementation file for CommissionEmployee class that represents an employee who is paid a percentage of gross sales. (Part 1 of 3.)*
