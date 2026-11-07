![](bbox=[0.309, 0.089, 0.771, 0.169])

*protected*, or *public*. Figure 11.4 shows these three types of inheritance in which B is the base class and D is the derived class.

The default type of inheritance is private. In other words, if we do not specify the type (*public*, *protected*, or *private*), the system assumes that we want private inheritance. Since private inheritance, as we will see later, is seldom used, we need to explicitly define the type of the inheritance. The most common is the public inheritance.

# 11.1.2 Public Inheritance

Although the default inheritance type is private inheritance, the most common, by far, is public inheritance. The other two types of inheritance are rarely used. We briefly discuss the other two types of inheritance later in the chapter, but in this section we concentrate on public inheritance. Some other object-oriented languages, like Java, have only public inheritance.

> **The most common use of inheritance is public inheritance.**

# EXAMPLE 11.1

In this example we design two classes, *Person* and *Student*, in which the class *Student* inherits from the class *Person*. We know that a student is a person. We assume that the *Person* class uses only one data member: *identity* (such as social security number). We also assume that the *Student* class needs two data members: *identity* and *gpa*. However, since the *identity* data member is already defined in the class *Person*, it does not need to be defined in the class *Student* because of inheritance. Figure 11.5 shows the extended UML class diagram with two compartments to accommodate the data members.

Based on Figure 11.5, we can immediately see the advantage of inheritance. The *Student* class uses the data member of the *Person* class and adds one data member of its own.

# EXAMPLE 11.2

In this example we add member functions to the two classes. We ignore the constructors and destructor at this point because they are not inherited; we assume the synthetic ones are

![](bbox=[0.351, 0.773, 0.731, 0.907])

**Figure 11.5**  Two classes in an inheritance relationship