# Chapter 12 OOP: Polymorphism and Interfaces

nerically. The only parts of an app that must be altered to accommodate new classes are those that require direct knowledge of the new classes that you add to the hierarchy. For example, if we extend Animal to create Tortoise (which might respond to a Move message by crawling one), we need to write only the Tortoise class and the part of the simulation that instantiates a Tortoise object. The portions of the simulation that process Animal generically can remain the same.

This chapter has several parts. First, we discuss common examples of polymorphism. As you will soon see, you will use base-class references to manipulate base-class objects and derived-class objects polymorphically.

# Polymorphic Employee Inheritance Hierarchy

We present a case study that revisits the Employee hierarchy of Section 11.4.5. We develop a payroll app that polymorphically calculates the weekly pay of several types of employees using each employee's Earnings. Although the earnings of each employee are calculated in a specific way, polymorphism allows us to process the employees "in general." In this case study, we include two new classes—SalariedEmployee (for people paid a fixed salary) and HourlyEmployee (for people paid an hourly salary and "time-and-half" for overtime). We declare a common functionality for all the classes in the updated hierarchy in a base class Employee. Hourly inherits directly and BasePlusCommissionEmployee inherits directly. As you will see, when we invoke each employee's Earnings method via a base-class reference, the correct calculation is performed by C#'s polymorphic capabilities.

# Determining the Type of an Object at Execution Time

Occasionally, when performing polymorphic processing, we need to program "in the spec." determine the type of object at execution time and act accordingly. In this case study, we use the capabilities to determine whether a particular employee object is a BasePlus-CommissionEmployee. If so, we increase that employee's base salary by 10%.

# Interfaces

The chapter continues with an introduction to C# interfaces. An interface describes a set of methods and properties that can be called on an object, but does not provide concrete implementations for them. You can declare classes that implement (i.e., provide concrete implementations for the methods and properties) one or more interfaces. Each interface member must be defined for all the classes that implement the interface. Once a class implements an interface, all objects of class have an is-relationship with the interface, and objects of the class are guaranteed to provide the functionality described by the interface. This is true of all derived classes of that class as well.

Interfaces are particularly useful for assigning functionality to objects of unrelated classes polymorphically—objects of classes that implement the same interface can respond to the same method. To demonstrate creating and using interfaces, we modify our payroll app to create a general accounts-payable app that calculates payments due for the earnings of company