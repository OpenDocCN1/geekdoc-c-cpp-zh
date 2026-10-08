# 10.1 Introduction

+   10.1 Introduction
10.2 Time Class Study; Throwing Exceptions
10.2.1 Time1 Class Declaration
10.2.2 Using Time1
10.3 Controlling Access to Members
10.4 Referring to the Current Object's Members with this Reference
10.5 Time Class Study: Overloaded Constructors
10.5.1 Time2 with Overloaded Constructors
10.5.2 Using Time2 with Overloaded Constructors
10.6 Default and Parameterless Constructors
10.7 Composition
10.7.1 Class Date
10.7.2 ClassEmployee

+   10.7.3 ClassEmployeeTest
10.8 Garbage Collection and Destructors
10.9 static Class Members
10.10 readonly Instance Variables
10.11 Class View and Object Browser
10.11.1 Using the Class View
10.11.2 Using the Object Browser
10.12 Object Initializers
10.13 Operator Overloading: Introducing struct
10.13.1 Creating Value Types with struct
10.13.2 Value Type ComplexNumber
10.13.3 Complex
10.14 Time Class Study: Extension Methods
10.15 Wrap-Up

![](bbox=[0.096, 0.127, 0.137, 0.203])

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 10.1 Introduction

In this chapter, we take a deeper look at building classes, controlling access to members of a class and creating constructors. We discuss composition—a capability that allows a class to have references to other classes as members. The chapter also discusses static class members and instance variables and properties.

We also introduce operator overloading. In previous chapters, we declared our classes and used methods to perform tasks on objects of those classes. Operator overloading allows us to define the behavior of the built-in operators, such as + and -, when used on objects of our own classes. This can provide a more convenient notation than calling methods for performing tasks (such as arithmetic) using objects.

We show how to create your own value types using struct, discuss key differences between structs and classes, and discuss when struct types should be used. Finally, we demonstrate how to create your extension methods to add functionality to an existing type that you did not define.

# 10.2 Time Class Study; Throwing Exceptions

Our first example consists of classes Time1 (Fig. 10.1) and TimeTest (Fig. 10.2). Class Time1 represents the time of day. TimeTest's main method creates an object of class Time1 and invokes its methods. The output of this appears in Fig. 10.2.

+   Cf has the types like DateTime and DateTime for date and time manipulations. Our examples are for demonstration purposes—you do not need to create your own types for dates and times. We use DateTime in Section 15.4.