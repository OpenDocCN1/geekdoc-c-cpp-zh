Chapter 1

# # How it works...

If you look at the main function, you'll notice that it doesn't differ from the program where you use integers, for example. Even though an integer is a primitive type and a complex is not, a programmer's work is made easier by adding a class and properly setting its methods.

Here we have defined a new type of class-CComplex. The defined class has its own attributes and methods. It can also have friend methods that can access its private members. We have left the Rand function as it is, but we tried to make the class that represents a complex number similar to the abstraction of a complex number. We created the dReal and ding attributes that describe the real and imaginary parts of a complex number. We created the operator+ so that the (plus) has meaning for the compiler. Now, the code is more readable and much more comfortable to use because it is easy to understand how to use it. The default constructor uses random numbers from -10 to 10, and another constructor enables the user to set the real and imaginary parts of a complex number.

When you want to overload (this will be explained in detail) a certain method, you can choose between two approaches. The first approach is to set the method inside a class, and this method will change the state (or values) of the calling object. The second approach is to make the method independent of the class, the so-called outer, but it has to be declared as friend so it can access the private and protected members of the objects.

# # There's more...

The following code tells the compiler the operator+ function which expects two complex numbers will be defined somewhere in the code, and it has to be able to access the private and protected members of the CComplex class:

```
friend CComplex operator+(const CComplex& c1, const CComplex& c2);
```

This makes the main function the simplest possible. Again, we use user-defined types as primitive types, which is very good practice because even programmers not familiar with the code will quickly understand what the code means.

# # Explaining inheritance, overloading, and overriding

Inheritance is a very important characteristic of OOP. It is the relation between two (or more) classes: if class B is some kind of class A, then the objects of class B have the same properties as the objects of class A. In addition to that, class B can implement new methods and thus supersede the base class A.

19