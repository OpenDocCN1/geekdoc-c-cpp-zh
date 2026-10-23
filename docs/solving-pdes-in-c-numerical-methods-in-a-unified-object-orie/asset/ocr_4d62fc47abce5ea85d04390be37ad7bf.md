the actual implementation of integer or real numbers in the hardware of the computer. Programmer B is not interested in the detailed implementation of the objects prepared by Programmer A. All that Programmer B needs are the objects themselves and the functions that operate upon them. Once these objects are available. Programmer B is free to use them in his particular application, regardless of their internal structure.

In fact, we could also consider a larger team of C++ programmers, in which Programmer A implements the objects required by all other programmers in their particular applications. Of course, Programmer A should also use feedback from these programmers to develop new functions that may be useful to potential users.

It is important that these programmers (or users) have a convenient interface to use the objects. This interface should not be changed, because any change in it would require changing every application that uses it. The actual implementation of objects, however, can be modified by Programmer A if necessary, so long as the modification doesn’t affect the interface. The users should have no access to the internal implementation of objects, or they could change it inadvertently and spoil the entire framework.

Thus, just as C programmers cannot change the properties of integer or real types, users of the objects prepared by Programmer A cannot change their properties or functions. The data structures used in the objects should be accessible to external users only through public interface functions implemented and maintained by Programmer A. In fact, even Programmer A cannot modify the implementation unless he/she makes sure that the public interface functions are called and used in the same way.

The minds of the users of the objects prepared by Programmer A are thus free to develop the algorithms required in their own applications. They can use these objects through the interface functions, with no concern about any detail of implementation. They can treat the objects as perfect abstract concepts, which is particularly useful in the development of new methods and approaches. This is particularly important in numerical modeling, where complex mathematical objects are often involved.

# 2.2 Classes

As discussed above, C++ is particularly suitable for implementing abstract mathematical structures, which can then be used by other programmers as new objects or types. Assume, for example, that one wants to implement a point in the two-dimensional Cartesian plane. The well-implemented point should then be used by external users as if it were a standard type such as "int" or "double", leaving the users completely unaware of how it is stored or manipulated. This would free the minds of the users to concentrate on their particular application without being distracted by the details of the implementation of the points.

In particular, users should be able to write commands like

```
point P;
point Q=P;
```

to define a point 'P' and use it to define and initialize another point 'Q'. As we’ll see below, this objective is achieved by defining the "point" class with its interface functions.

A new object in C++ is defined in a class as follows:

```
class point{
public:
```