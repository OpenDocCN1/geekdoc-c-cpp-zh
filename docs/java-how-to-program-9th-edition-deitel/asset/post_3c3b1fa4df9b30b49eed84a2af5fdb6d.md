
method calls. To demonstrate creating and using interfaces, we modify our payroll application to create a general accounts payable application that can calculate payments due for company employees and invoice amounts to be billed for purchased goods. As you’ll see, interfaces enable polymorphic capabilities similar to those possible with inheritance.

## 10.2 Polymorphism Examples

We now consider several additional examples of polymorphism.

### Quadrilaterals

If class Rectangle is derived from class Quadrilateral, then a Rectangle object is a more specific version of a Quadrilateral. Any operation (e.g., calculating the perimeter or the area) that can be performed on a Quadrilateral can also be performed on a Rectangle. These operations can also be performed on other Quadrilaterals, such as Squares, Parallelograms and Trapezoids. The polymorphism occurs when a program invokes a method through a superclass Quadrilateral variable—at execution time, the correct subclass version of the method is called, based on the type of the reference stored in the superclass variable. You’ll see a simple code example that illustrates this process in Section 10.3.

### Space Objects in a Video Game

Suppose we design a video game that manipulates objects of classes Martian, Venusian, Plutonian, SpaceShip and LaserBeam. Imagine that each class inherits from the superclass SpaceObject, which contains method draw. Each subclass implements this method. A screen manager maintains a collection (e.g., a SpaceObject array) of references to objects of the various classes. To refresh the screen, the screen manager periodically sends each object the same message—namely, draw. However, each object responds its own way, based on its class. For example, a Martian object might draw itself in red with green eyes and the appropriate number of antennae. A SpaceShip object might draw itself as a bright silver flying saucer. A LaserBeam object might draw itself as a bright red beam across the screen. Again, the *same message* (in this case, *draw*) sent to a variety of objects has “many forms” of results.

A screen manager might use polymorphism to facilitate adding new classes to a system with minimal modifications to the system’s code. Suppose that we want to add Mercurian objects to our video game. To do so, we’d build a class Mercurian that extends SpaceObject and provides its own draw method implementation. When Mercurian objects appear in the SpaceObject collection, the screen manager code *invokes method draw, exactly as it does for every other object in the collection, regardless of its type.* So the new Mercurian objects simply “plug right in” without any modification of the screen manager code by the programmer. Thus, without modifying the system (other than to build new classes and modify the code that creates new objects), you can use polymorphism to conveniently include additional types that were not envisioned when the system was created.

> **Software Engineering Observation 10.1**
> 
> *Polymorphism enables you to deal in generalities and let the execution-time environment handle the specifics. You can command objects to behave in manners appropriate to those objects, without knowing their types (as long as the objects belong to the same inheritance hierarchy).*

## Software Engineering Observation 10.2

Polymorphism promotes extensibility: Software that invokes polymorphic behavior is independent of the object types to which messages are sent. New object types that can respond to existing method calls can be incorporated into a system without modifying the base system. Only client code that instantiates new objects must be modified to accommodate new types.

## 10.3 Demonstrating Polymorphic Behavior

Section 9.4 created a class hierarchy, in which class BasePlusCommissionEmployee inherited from CommissionEmployee. The examples in that section manipulated CommissionEmployee and BasePlusCommissionEmployee objects by using references to them to invoke their methods—we aimed superclass variables at superclass objects and subclass variables at subclass objects. These assignments are natural and straightforward—superclass variables are intended to refer to superclass objects, and subclass variables are intended to refer to subclass objects. However, as you’ll soon see, other assignments are possible.

In the next example, we aim a superclass reference at a subclass object. We then show how invoking a method on a subclass object via a superclass reference invokes the subclass functionality—the type of the referenced object, not the type of the variable, determines which method is called. This example demonstrates that an object of a subclass can be treated as an object of its superclass, enabling various interesting manipulations. A program can create an array of superclass variables that refer to objects of many subclass types. This is allowed because each subclass object is an object of its superclass. For instance, we can assign the reference of a BasePlusCommissionEmployee object to a superclass CommissionEmployee variable, because a BasePlusCommissionEmployee is a CommissionEmployee—we can treat a BasePlusCommissionEmployee as a CommissionEmployee.

As you’ll learn later in the chapter, you cannot treat a superclass object as a subclass object, because a superclass object is not an object of any of its subclasses. For example, we cannot assign the reference of a CommissionEmployee object to a subclass BasePlusCommissionEmployee variable, because a CommissionEmployee is not a BasePlusCommissionEmployee—a CommissionEmployee does not have a baseSalary instance variable and does not have methods setBaseSalary and getBaseSalary. The is-a relationship applies only up the hierarchy from a subclass to its direct (and indirect) superclasses, and not vice versa (i.e., not down the hierarchy from a superclass to its subclasses).

The Java compiler does allow the assignment of a superclass reference to a subclass variable if we explicitly cast the superclass reference to the subclass type—a technique we discuss in Section 10.5. Why would we ever want to perform such an assignment? A superclass reference can be used to invoke only the methods declared in the superclass—attempting to invoke subclass-only methods through a superclass reference results in compilation errors. If a program needs to perform a subclass-specific operation on a subclass object referenced by a superclass variable, the program must first cast the superclass reference to a subclass reference through a technique known as downcasting. This enables the program to invoke subclass methods that are not in the superclass. We show a downcasting example in Section 10.5.

The example in Fig. 10.1 demonstrates three ways to use superclass and subclass variables to store references to superclass and subclass objects. The first two are straightforward—as in Section 9.4, we assign a superclass reference to a superclass variable, and a subclass reference to a subclass variable. Then we demonstrate the relationship between subclasses and superclasses (i.e., the is-a relationship) by assigning a subclass reference to a superclass variable. This program uses classes CommissionEmployee and BasePlusCommissionEmployee from Fig. 9.10 and Fig. 9.11, respectively.

```
// Fig. 10.1: PolymorphismTest.java
// Assigning superclass and subclass references to superclass and
// subclass variables.

public class PolymorphismTest
{
    public static void main( String[] args )
    {
        // assign superclass reference to superclass variable
        CommissionEmployee commissionEmployee = new CommissionEmployee(
            "Sue", "Jones", "222-22-2222", 10000, .06 );

        // assign subclass reference to subclass variable
        BasePlusCommissionEmployee basePlusCommissionEmployee =
            new BasePlusCommissionEmployee(
            "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );

        // invoke toString on superclass object using superclass variable
        System.out.printf( "%s %s:\n\n%s\n\n",
            "Call CommissionEmployee's toString with superclass reference ",
            "to superclass object", commissionEmployee.toString() );

        // invoke toString on subclass object using subclass variable
        System.out.printf( "%s %s:\n\n%s\n\n",
            "Call BasePlusCommissionEmployee's toString with subclass",
            "reference to subclass object",
            basePlusCommissionEmployee.toString() );

        // invoke toString on subclass object using superclass variable
        CommissionEmployee commissionEmployee2 =
            basePlusCommissionEmployee;
        System.out.printf( "%s %s:\n\n%s\n",
            "Call BasePlusCommissionEmployee's toString with superclass",
            "reference to subclass object", commissionEmployee2.toString() );
    } // end main
} // end class PolymorphismTest
```

Call CommissionEmployee's toString with superclass reference to superclass object:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

Fig. 10.1 | Assigning superclass and subclass references to superclass and subclass variables.
(Part 1 of 2.)
