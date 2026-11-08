For example, suppose you have defined a Carton class and want to allow the member functions of the Carton class to have access to the members of the Box class. Including a statement in the Box class definition that declares Carton to be a friend will enable this:

```
```cpp
class Box
{
    // Public members of the class...

    friend class Carton;

    // Private members of the class...
};
```
```

Friendship is not a reciprocal arrangement. Functions in the Carton class can access all the members of the Box class, but functions in the Box class have no access to the private members of the Carton class. Friendship among classes is not transitive either; just because class A is a friend of class B and class B is a friend of class C, it doesn’t follow that class A is a friend of class C.

A typical use for a friend class is where the functioning of one class is highly intertwined with that of another. A linked list basically involves two class types: a List class that maintains a list of objects (usually called nodes) and a Node class that defines what a node is. The List class needs to stitch the Node objects together by setting a pointer in each node object so that it points to the next Node object. Making the List class a friend of the class that defines a node would enable members of the List class to access the members of the Node class directly. Later in this chapter we’ll discuss nested classes, a viable alternative for friend classes in such cases.

# ## Arrays of Class Objects

You can create an array of objects of a class type in the same way as you create an array of elements of any other type. Each array element has to be created by a constructor, and for each element that does not have an initial value specified, the compiler arranges for the no-arg constructor to be called. You can see this happening with an example. The Box class definition in Box.cpp is as follows:

```
```cpp
// Box.cpp
export module box;

export class Box
{
public:
    /* Constructors */
    Box(double length, double width, double height);
    Box(double side);          // Constructor for a cube
    Box();                     // Default constructor
    Box(const Box& box);       // Copy constructor

    double volume() const { return m_length * m_width * m_height; };

private:
    double m_length {1.0};
    double m_width {1.0};
    double m_height {1.0};
};
```
```