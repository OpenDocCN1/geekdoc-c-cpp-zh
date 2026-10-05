# 21 • More about Inheritance 691

For convenience, I declared the l and h members as protected so that derived classes may access them directly. As an alternative to the example of C.20.12, in order to manage objects of both Triangle and Rectangle classes with one entity and outlet polymorphism I chose to use a vector of pointers to the base class Shape. As shown, a pure virtual function has no definition. Its purpose is to enable the versions of the function in the derived classes to be called polymorphically.

A class that contains at least one pure virtual function (e.g., Shape) is called abstract. An abstract class can contain only one pure virtual functions. Notice that it is not allowed to create objects of an abstract class. That is, if

Shape s(1,2); the compiler will display an error. The rational of an abstract class is that it is used only as base; it is a concept that represents the common characteristics of related entities.

Since we cannot create, it is not allowed to pass its value in a function or return an object as parameters or return type. In this, it is essential to exploit the polymorphic behaviour of the virtual functions. Well, a question arises, since we cannot create objects, why does the Shape contain a constructor? Is it there to initialize its member variables. And who is going to call it? It will be called by the constructors of the derived classes in order to build the Shape sub-objects they contain.

A pure virtual not defined in the derived class is still considered to be pure virtual. Thus, the derived class abstract too. For example:

```
class A
{
    virtual void f() = 0;
    virtual void g() = 0;
};
class B : public A
{
    virtual void g() {}; // f() is still pure virtual.
};
class C : public B
{
    virtual void f() {};
};
```

B b; /* Wrong, B is an abstract class. It is not allowed to create objects.
C c; // Correct.

Since g() is not defined in B, B becomes an abstract class, so it is not allowed to create objects of this class.
The programming model based on the concept of abstraction is quite common. To return to this, the common elements resulting from the design of the classes are placed in a base class, while the functions implemented in each derived class are declared as pure virtual. This design avoids duplication of the same code and thus, facilitates the maintenance and upgrade of the program. In general, abstract classes tend to contain only pure virtual functions (data members are defined in the derived classes) and consequently no constructors (since there are no data members to initialize, it is unlikely to need a constructor). Essentially, an abstract class is a kind of contract for what a derived class should provide. The abstract class “what needs to be implemented”, leaving the implementation tasks of the virtual functions to the programmer of each derived class.