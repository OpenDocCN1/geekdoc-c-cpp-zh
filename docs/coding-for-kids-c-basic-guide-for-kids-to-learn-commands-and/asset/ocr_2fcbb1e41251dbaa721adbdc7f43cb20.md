# # Chapter 8: Class and Objects in C++

In this chapter, we will learn about objects and classes and how to utilize them in C++ with the help of examples.

We studied functions and variables in an earlier chapter. It is sometimes preferable to group together relevant functions and data to be more logical and easier to work with.

Assume we need to compute the area and volume of a rectangular room based on its length, breadth, and height.

We can use three variables, such as length, width, and height, as well as the functions, calculate area() and calculate volume() to complete this work ().

Instead of defining distinct variables and functions in C++, we can wrap these related data and functions in a single location (by creating objects). Object-oriented programming is the name for this programming paradigm.

However, before we can build and use objects in C++, we must first understand classes.

# ## 8.1 C++ Class

In C++, a class is the fundamental building block of Object-Oriented programming. It is a user-defined data type with its own set of data members and member functions that can be accessed and used by establishing a class instance. A C++ class is similar to an object's blueprint.

Consider the following scenario: Consider the Automobile Class. There may be many automobiles with different names and brands, but they will all have some essential characteristics, such as four wheels, a speed limit, and mileage range. Car is the class here, and wheels, speed limitations, and mileage are the attributes.

+   - A Class is a data type that has data members and member functions that the user defines.
+   - Data members are data variables, and member functions are the functions that control these variables; these data members and member functions together define the properties and behavior of the objects in a Class.
+   - The data members in the previous example of class Car will be speed limit, mileage, and member functions will apply brakes, increase speed, and so on.
+   - The sole difference between a class and a structure in C++ is that a class defaults to private access control, whereas a structure defaults to public.
+   - All of OOPS' features revolve around C++ classes. Inheritance, encapsulation, abstraction, and other concepts are discussed.
+   - Separate copies of data members are stored in class objects. We can make as many class objects as we need.
+   - Classes have additional qualities, such as the ability to build abstract and immutable classes, which we shall cover later.

**For example**, all birds in the class of birds can fly and have wings and beaks. So, in this case, flying is a habit, and wings and beaks are features. Moreover, while there are many distinct birds in this class, all of them share the same behavior and traits.

Similarly, a class is nothing more than a blueprint that declares and defines traits and behavior, such as data members and member functions. These characteristics and behaviors will be shared by all objects in this class.