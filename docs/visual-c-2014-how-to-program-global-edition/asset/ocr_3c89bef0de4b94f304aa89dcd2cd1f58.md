# Chapter 12 OOP: Polymorphism and Interfaces

typically do not need to worry about the specifics, or to adjust the base salary, we
have to determine the type of each Employee object at execution time. Line 44 uses
t is operator to determine whether a particular Employee object's type is BasePlusCom-\missionEmployee. The condition in line 44 is true if the object referenced by
CurrentEmployee is a BasePlusCommissionEmployee. This would also be true for any ob-\ject a BasePlusCommissionEmployee derived class (if there were any), because an object
of any BasePlusCommissionEmployee derived class is a BasePlusCommissionEmployee.

Line 48 casts result from Employee type to type to BasePlusCommissionEm-
ployee assigns as a downcast, because the cast is a type lower down the class hierarchy.
downcast is allowed only if the object to which Employee refers has an is-rela-
ship with BasePlusCommissionEmployee--the condition at line 44 ensures this is the
case. Why we need to perform such a downcast? A base-class reference can be
used to invoke the methods declared in the base class--attempting to invoke a derived-
-only method through a base-class reference results in a compilation error. If an app
eeds to perform a derived-class operation on a derived-class object referenced by
a base-class variable, the must first cast the base-class reference to a derived-class-
erference, so this is required in this program for us to use derived BasePlusCom-
missionEmployee's BaseSalary on the currentEmployee.

# Common Programming Error 12.3

Assigning a base-class variable to a derived-class variable (without an explicit downcast)
is a compilation error.

# Software Engineering Observation 12.5

If at execution time the reference to a derived-class object has been assigned to a variable
ofne of its direct or indirect base classes, it's acceptable to cast the reference stored in that-
class variable back to a reference of the derived-class type. Before performing such a cast, use
is the operator to ensure that the object is indexed an object of an appropriate derived-class
type.

When downcasting at execution time the object does not have an is-relationship with the type spec-
ified in the cast, an InvalidCastException occurs. An object can be cast to its own type or to one of
of its classes. You can avoid a potential InvalidCastException by using the as
to to perform a downcast rather than a cast. For example, in the

```
var employee = currentEmployee as BasePlusCommissionEmployee;
```

employee assigned is a reference to object that is BasePlusCommissionEmployee, or
the null if currentEmployee is not a BasePlusCommissionEmployee. You can then
compare with null to determine whether the cast was succeeded.

If the expression in line 44 is true, the lines (44--53) performs the
special proceeding required for the BasePlusCommissionEmployee object. Using Base-
PlusCommissionEmployee variable employee, line 50 accesses the derived-class-only prop-\ertyBaseSalary to retrieve and update the employee's salary with the 10% increase.
Line 55 invokes method Earnings on currentEmployee, which calls the appropriate
derived-class object's Earnings method polymorphically. Obtaining the earnings of the Sal-