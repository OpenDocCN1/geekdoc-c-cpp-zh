class. You can also inherit a class from multiple base classes, separated by commas. This type of inheritance is known as multiple inheritance.

In this chapter, you learn about the mechanism of inheritance by using base and derived classes, and the protected access specifier. You also learn about the three types of derivations: private, protected, and public, and how a derived class overrides the members of the base class. In addition, you learn about the order in which constructors and destructors are invoked when inheritance is implemented as well as about container classes. The chapter also discusses different forms of inheritance, such as single inheritance, multiple inheritance, and multilevel inheritance. It explains the problems that arise for a compiler when multiple inheritance is implemented. Next, you learn how to create and use pointer objects of base and derived classes to access their members. The chapter concludes with a description of the concept of binding and the implementation of dynamic binding with the concepts of virtual functions, pure virtual functions, and abstract classes.

Let’s start by exploring the concept of base and derived classes in inheritance.

# 7.1  Exploring the Concept of Base and Derived Classes

As mentioned earlier, a class that inherits or derives its features from another class is called a derived class, and the class from which it is derived is called a base class. The base class is also called a super class, and a derived class is called a subclass.

An instance of a derived class includes most of the features of the base class. Therefore, a derived class may contain a larger set of features than its base class. A derived class can modify some or all the inherited features of the base class. Figure 1 shows the relationship between a base class (Car) and a derived class (Maruti Zen):

![](bbox=[0.332, 0.547, 0.842, 0.804])

▲ Figure 1: Displaying Relationship between Base Class and Derived Class