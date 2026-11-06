# Observation 11.7

*Suppose that we create an object of a derived class where both the base class and the derived class contain (via composition) objects of other classes. When an object of that derived class is created, first the constructors for the base class’s member objects execute, then the base-class constructor body executes, then the constructors for the derived class’s member objects execute, then the derived class’s constructor body executes. Destructors for derived-class objects are called in the reverse of the order in which their corresponding constructors are called.*

By default, base-class constructors, destructors and overloaded assignment operators (**Chapter 10**) are *not* inherited by derived classes. Derived-class constructors, destructors and overloaded assignment operators, however, can call base-class versions.

# C++11: *Inheriting Base-Class Constructors*

Sometimes a derived class’s constructors simply specify the same parameters as the base class’s constructors and simply pass the constructor arguments to the base-class’s constructors. For such cases, C++11 allows you to specify that a derived class should *inherit* a base class’s constructors. To do so, *explicitly* include a `using` declaration of the form