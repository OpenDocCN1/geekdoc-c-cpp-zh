# CHAPTER 6 Structures and Classes

> TIP: Thinking Objects

If you have not programmed with classes before, it can take a little while to get the feel of programming with them. When you program with classes, data rather than algorithms take center stage. It is not that there are no algorithms. However, the algorithms are made to fit the data, as opposed to designing the data to fit the algorithms. It is a difference in point of view. In the extreme case, which is considered many to be the best style, you have no global functions at all, only classes with member functions. In this case, you define objects and how the objects interact, rather than algorithms that operate on data. We will discuss the details of how you accomplish this throughout this book. Of course, you can ignore classes completely or relegate them to a minor role, but then you are really programming in C, not C++.

# Self-Test Exercises

+   16. When you define a C++ class, should you make the member variables public or private? Should you make the member functions public or private?
17. When you define a C++ class, what items are considered part of the interface? What items are considered part of the implementation?

# Chapter Summary

+   * A structure can be used to combine data of different types into a single (compound) data value.
* A class can be used to combine data and functions into a single (compound) object.
* A member variable or member function for a class can be either public or private. If it is public, it can be used outside the class. If it is private, it can be used only in the definition of a member function.
* A function can have formal parameters of a class or structure type. A function can return values of a class or structure type.
* A member function for a class can be overloaded in the same way as ordinary functions are overloaded.
* When defining a C++ class, you should separate the interface and implementation so that any programmer who uses the class need only know the interface and not even look at the implementation. This is the principle of encapsulation.