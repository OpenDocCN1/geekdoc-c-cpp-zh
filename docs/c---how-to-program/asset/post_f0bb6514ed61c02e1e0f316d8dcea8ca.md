
```cpp
9  HugeInt n1( 7654321 );
10 HugeInt n2( 7891234 );
11 HugeInt n3( "9999999999999999999999999" );
12 HugeInt n4( "1" );
13 HugeInt n5;

14
15 cout << "n1 is " << n1 << "\n\n" << "n2 is " << n2
16     << "\n\n" << "n3 is " << n3 << "\n\n" << "n4 is " << n4
17     << "\n\n" << "n5 is " << n5 << "\n\n";

18 n5 = n1 + n2;

19
20 cout << n1 << " + " << n2 << " = " << n5 << "\n\n";
21
22 cout << n3 << " + " << n4 << " = " << ( n3 + n4 ) << "\n\n";
23
24 n5 = n1 + 9;
25 cout << n1 << " + " << 9 << " = " << n5 << "\n\n";
26
27 n5 = n2 + "10000";
28 cout << n2 << " + " << "10000" << " = " << n5 << endl;
29 } // end main
```

```text
n1 is 7654321
n2 is 7891234
n3 is 9999999999999999999999999
n4 is 1
n5 is 0

7654321 + 7891234 = 15545555

9999999999999999999999999 + 1
= 10000000000000000000000000

7654321 + 9 = 7654330

7891234 + 10000 = 7901234
```

**Fig. 18.19** | HugeInt test program. (Part 2 of 2.)

### 18.10 (RationalNumber Class)

Create a class RationalNumber (fractions) with these capabilities:

- a) Create a constructor that prevents a 0 denominator in a fraction, reduces or simplifies fractions that are not in reduced form and avoids negative denominators.
- b) Overload the addition, subtraction, multiplication and division operators for this class.
- c) Overload the relational and equality operators for this class.

### 18.11 (Polynomial Class)

Develop class Polynomial.

The internal representation of a Polynomial is an array of terms. Each term contains a coefficient and an exponent, e.g., the term 2x⁴ has the coefficient 2 and the exponent 4. Develop a complete class containing proper constructor and destructor functions as well as set and get functions. The class should also provide the following overloaded operator capabilities:

- a) Overload the addition operator (+) to add two Polynomials.
- b) Overload the subtraction operator (-) to subtract two Polynomials.
- c) Overload the assignment operator (=) to assign one Polynomial to another.
- d) Overload the multiplication operator (*) to multiply two Polynomials.
- e) Overload the addition assignment operator (+=), subtraction assignment operator (-=), and multiplication assignment operator (*=).

## 19 Object-Oriented Programming: Inheritance

### Objectives

In this chapter you'll learn:

- What inheritance is and how it promotes software reuse.
- The notions of base classes and derived classes and the relationships between them.
- The protected member access specifier.
- The use of constructors and destructors in inheritance hierarchies.
- The order in which constructors and destructors are called in inheritance hierarchies.
- The differences between `public`, `protected` and `private` inheritance.
- To use inheritance to customize existing software.

### Outline

- 19.1 Introduction
- 19.2 Base Classes and Derived Classes
- 19.3 Relationship between Base and Derived Classes
  - 19.3.1 Creating and Using a CommissionEmployee Class
  - 19.3.2 Creating a BasePlusCommissionEmployee Class Without Using Inheritance
  - 19.3.3 Creating a CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy
  - 19.3.4 CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy Using protected Data
  - 19.3.5 CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy Using private Data
- 19.4 Constructors and Destructors in Derived Classes
- 19.5 public, protected and private Inheritance
- 19.6 Software Engineering with Inheritance
- 19.7 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

### 19.1 Introduction

This chapter continues our discussion of object-oriented programming (OOP) by introducing inheritance—a form of software reuse in which you create a class that absorbs an existing class’s capabilities, then customizes or enhances them. Software reuse saves time during program development by taking advantage of proven, high-quality software.

When creating a class, instead of writing completely new data members and member functions, you can specify that the new class should inherit the members of an existing class. This existing class is called the base class, and the new class is called the derived class. Other programming languages, such as Java and C#, refer to the base class as the superclass and the derived class as the subclass. A derived class represents a more specialized group of objects.

C++ offers public, protected and private inheritance. In this chapter, we concentrate on public inheritance and briefly explain the other two. With public inheritance, every object of a derived class is also an object of that derived class’s base class. However, base-class objects are not objects of their derived classes. For example, if we have Vehicle as a base class and Car as a derived class, then all Cars are Vehicles, but not all Vehicles are Cars—for example, a Vehicle could also be a Truck or a Boat.

We distinguish between the is-a relationship and the has-a relationship. In an is-a relationship, an object of a derived class also can be treated as an object of its base class—for example, a Car is a Vehicle, so any attributes and behaviors of a Vehicle are also attributes and behaviors of a Car. By contrast, the has-a relationship represents composition, which was discussed in Chapter 17. In a has-a relationship, an object contains one or more objects of other classes as members. For example, a Car has many components—it has a steering wheel, has a brake pedal, has a transmission, etc.

### 19.2 Base Classes and Derived Classes

Figure 19.1 lists some simple examples of base classes and derived classes. Base classes tend to be more general and derived classes tend to be more specific.

| Base class | Derived classes |
|---|---|
| Student | GraduateStudent, UndergraduateStudent |
| Shape | Circle, Triangle, Rectangle, Sphere, Cube |
| Loan | CarLoan, HomeImprovementLoan, MortgageLoan |
| Employee | Faculty, Staff |
| Account | CheckingAccount, SavingsAccount |

**Fig. 19.1** | Inheritance examples.

Because every derived-class object is an object of its base class, and one base class can have many derived classes, the set of objects represented by a base class typically is larger than the set of objects represented by any of its derived classes. For example, the base class Vehicle represents all vehicles, including cars, trucks, boats, airplanes, bicycles and so on. By contrast, derived class Car represents a smaller, more specific subset of all vehicles.

Inheritance relationships form class hierarchies. A base class exists in a hierarchical relationship with its derived classes. Although classes can exist independently, once they're employed in inheritance relationships, they become affiliated with other classes. A class becomes either a base class—supplying members to other classes, a derived class—inheriting its members from other classes, or both.

**CommunityMember Class Hierarchy**

Let's develop a simple inheritance hierarchy with five levels (represented by the UML class diagram in Fig. 19.2). A university community has thousands of CommunityMembers.

These CommunityMembers consist of Employees, Students and alumni (each of class Alumnus). Employees are either Faculty or Staff. Faculty are either Administrators or Teachers. Some Administrators, however, are also Teachers. We've used *multiple inheritance* to form class AdministratorTeacher. With single inheritance, a class is derived from *one* base class. With multiple inheritance, a derived class inherits simultaneously from *two or more* (possibly unrelated) base classes. Multiple inheritance is generally discouraged.

![](img/d0d3b7423c2d9e5650be79209ea1885d_766_0.png)

**Fig. 19.2** | Inheritance hierarchy for university CommunityMembers.

Each arrow in the hierarchy (Fig. 19.2) represents an *is-a* relationship. For example, as we follow the arrows in this class hierarchy, we can state "an Employee is a CommunityMember" and "a Teacher is a Faculty member." CommunityMember is the direct base class of Employee, Student and Alumnus. In addition, CommunityMember is an indirect base class of all the other classes in the diagram. An indirect base class is inherited from two or more levels up the class hierarchy.

Starting from the bottom of the diagram, you can follow the arrows upwards and apply the *is-a* relationship to the topmost base class. For example, an AdministratorTeacher is an Administrator, is a Faculty member, is an Employee and is a CommunityMember.

**Shape Class Hierarchy**

Now consider the Shape inheritance hierarchy in Fig. 19.3. This hierarchy begins with base class Shape. Classes TwoDimensionalShape and ThreeDimensionalShape derive from base class Shape—a Shape *is a* TwoDimensionalShape or *is a* ThreeDimensionalShape. The third level of this hierarchy contains more specific types of TwoDimensionalShapes and ThreeDimensionalShapes. As in Fig. 19.2, we can follow the arrows from the bottom of the diagram upwards to the topmost base class in this hierarchy to identify several *is-a* relationships. For instance, a Triangle *is a* TwoDimensionalShape and *is a* Shape, while a Sphere *is a* ThreeDimensionalShape and *is a* Shape.

![](img/d0d3b7423c2d9e5650be79209ea1885d_767_0.png)

**Fig. 19.3** | Inheritance hierarchy for Shapes.

To specify that class TwoDimensionalShape (Fig. 19.3) is derived from (or inherits from) class Shape, class TwoDimensionalShape's definition could begin as follows:

```
class TwoDimensionalShape : public Shape
```

This is an example of public inheritance, the most commonly used form. We'll also discuss private inheritance and protected inheritance (Section 19.5). With all forms of inheritance, private members of a base class are *not* accessible directly from that class's derived classes, but these private base-class members are still inherited (i.e., they're still considered parts of the derived classes). With public inheritance, all other base-class members retain their original member access when they become members of the derived class.
