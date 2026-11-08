# Chapter 5 Constructors, Destructors, and Operators

# Overview

C++ constructors are more complicated than their C# counterparts. For one thing, there are five types of constructors. Although you will rarely write all five types for any particular class or structure, you do need to know what they are, what they do, and what they look like. If not, you could find yourself facing some very confusing bugs or compiler errors.

The reason C++ constructors are more involved than C# constructors is the variety in storage duration that a C++ class can have. By default, C++ objects have value semantics while C# classes have reference semantics. Here’s an example:

```
```cpp
Vehicle someVehicle = vehicle;
```
```

Let’s assume vehicle is not null but is a valid object of type Vehicle, and that the Vehicle type is a class type as opposed to a structure or something else.

Let’s consider the previous code statement as if it were C# code. In C#, the object that vehicle refers to lives off somewhere in a heap managed by the GC. The previous code statement stores a reference to that object in the someVehicle variable, which it gets from the existing vehicle reference to the object. There is still just the one instance of that object with two references to it.

Let’s now consider the previous statement as if it were C++ code. In C++, the object that vehicle refers to is likely an automatic duration object, but it could be a static duration object or even a thread duration object. The previous code statement would by default create a copy of the vehicle object and store it in the address of the automatic duration someVehicle variable. It does this using something called a copy assignment operator, a close relative of a copy constructor.

There are now two copies where once there was one. Unless the Vehicle class has a pointer, a `std::shared_ptr`, a reference, or something of that sort as a member variable, the two copies are completely separate. Changing or even destroying one will have no effect whatsoever on the other.

Of course, if you want someVehicle to be a reference to vehicle’s object, you can change the code slightly and accomplish that. But what if you wanted someVehicle to become vehicle and for vehicle to stop existing—to be destroyed without taking its former resources with it? C++ makes this possible through something called a move constructor and a move assignment operator.

If you want to intentionally disable copy semantics (assignment and construction, collectively) or move semantics, that is possible too.

# Default Constructor

We’ll start with default constructors. A default constructor can be called with no arguments. A class can have no more than one default constructor. If you define a class and include no constructors, you produce an implicit default constructor, which the compiler creates for you. However, if you have a class member variable that is a class, structure, or union that has no default constructor, then you must define at least one constructor because the compiler cannot create an implicit default constructor.