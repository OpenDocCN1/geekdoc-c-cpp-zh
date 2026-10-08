# 476 Chapter II Object-Oriented Programming: Inheritance

+   11.1 Introduction
11.2 Base Classes and Derived Classes
11.3 Protected Members
11.4 Relationship between Base Classes and Derived Classes
11.4.1 Creating and Using a Employee Class
11.4.2 Creating a BasePlusEmployee Class Without Using Inheritance
11.4.3 Creating a CommissionEmployee-Inheritance Hierarchy
11.44 CommissionEmployeeBasePlusEmployee Inheritance Using protected Instance Variables
11.45 CommissionEmployeeBasePlusEmployee Inheritance Hierarchy Using private Instance Variables
11.5 Constructors in Derived Classes
11.6 Software Engineering with Inheritance
11.7 Class object
11.8 Wrap-Up
Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

![](bbox=[0.098, 0.122, 0.135, 0.269])

# # 11.1 Introduction

This chapter continues our discussion of object-oriented programming (OOP) by introducing one of its primary features—inheritance, a form of software reuse in which a new class is created by absorbing existing class's members and enhancing them with new or modified capabilities. Inheritance lets you save time during development by reusing proven, high-performance and debugged-quality software. This also increases the likelihood that a system will be implemented effectively.

The existing class from which new class inherits is the base class, and the new class is the derived class. A derived class normally adds its own fields, properties and methods. Therefore, it's more specific than its base class and represents a more specialized group of objects. The derived class exhibits the behaviors of its base class and additional ones that are specific to it.

The direct base class is the class from which a derived class inherits the direct base class in the class hierarchy defines the inheritance relationships between classes. Section 11.7 lists class object—a C# keyword that's an alias for System.Object in the Framework Class Library. Every directly or indirectly extends (or inherits from) that object. Section 11.7 lists class object's methods, which every other class inherits. In single inheritance, a class is derived only once. C# supports from one direct base class. In Chapter 12, we explain how to use interfaces to realize many of the benefits of multiple inheritance (i.e., inheriting from multiple base classes) avoiding the associated problems that occur in some programming languages.

Building in software systems indicates that significant amounts of code with closely related special cases. When you're preoccupied with special cases, the details can obscure the picture. With object-oriented programming, you can, appropriate for the commonalities among objects in the system rather than the special cases.

We distinguish between the is-a relationship and the has-a relationship. In an is-relationship, an object of a derived class can also be treated as an object of its base class. For example, a car is a vehicle and a truck is a vehicle by.