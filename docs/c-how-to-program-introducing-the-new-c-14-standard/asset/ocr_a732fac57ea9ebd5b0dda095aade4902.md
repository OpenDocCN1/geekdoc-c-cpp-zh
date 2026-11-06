# 9.15.3 Accessing `static` Data Members

A class’s `private` (and `protected`; **Chapter 11**) `static` members are normally accessed through the class’s `public` member functions or `friend`s. A class’s *static* members exist even when no objects of that class exist. To access a `public static` class member when no objects of the class exist, simply prefix the class name and the scope resolution operator (`::`) to the name of the data member. For example, if our preceding variable `martianCount` is `public`, it can be accessed with the expression `Martian::martianCount`, even when there are no `Martian` objects. (Of course, using `public` data is discouraged.)

To access a `private` or `protected static` class member when *no* objects of the class exist, provide a `public` **static member function** and call the function by prefixing its name with the class name and scope resolution operator. A `static` member function is a service of the class, *not* of a specific *object* of the class.

![](bbox=[0.118, 0.777, 0.194, 0.837])

# *Software Engineering Observation*

*9.12*