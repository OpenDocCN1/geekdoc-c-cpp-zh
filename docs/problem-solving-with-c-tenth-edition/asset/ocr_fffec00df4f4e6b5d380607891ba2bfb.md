(when you do not define =); it will not have anything to do with the base class assignment operator defined in Base.

It is natural that constructors, destructors, and the assignment operator are not inherited. To correctly perform their tasks, they need information that the base class does not possess. To correctly perform their functions, they need to know about the new member variables introduced in the derived class.

# Assignment Operators and Copy Constructors in Derived Classes

Overloaded assignment operators and constructors are not inherited. However, they can be, and in almost all cases must be, used in the definitions of overloaded assignment operators and copy constructors in derived classes.

When overloading the assignment operator in a derived class, you normally use the overloaded assignment operator from the base class. We will present an outline of how the code for doing this is written. To help understand the code outline, remember that an overloaded assignment operator must be defined as a member function of the class.

If Derived is a class derived from Base, then the definition of the overloaded assignment operator for the class Derived would typically begin with something like the following:

```
Derived& Derived::operator =(const Derived& rightSide)
{
    Base::operator =(rightSide);
}
```

The first line of code in the body of the definition is a call to the overloaded assignment operator of the Base class. This takes care of the inherited member variables and their data. The definition of the overloaded assignment operator would then go on to set the new member variables that were introduced in the definition of the class Derived.

A similar situation holds for defining the copy constructor in a derived class. If Derived is a class derived from Base, then the definition of the copy constructor for the class Derived would typically use the copy constructor for the class Base to set up the inherited member variables and their data. The code would typically begin with something like the following:

```
Derived::Derived(const Derived& object)
    : Base(object), <probably more initializations>
{
```

The invocation of the base class copy constructor Base(object) sets up the inherited member variables of the Derived class object being created. Note that since object is of type Derived, it is also of type Base; therefore, object is a legal argument to the copy constructor for the class Base.

Of course, these techniques do not work unless you have a correctly functioning assignment operator and a correctly functioning copy constructor for