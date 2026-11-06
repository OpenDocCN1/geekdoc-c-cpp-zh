class pointer `bp` is going to be called when `delete bp` is executed. Thus, late binding is realized for destructors even though the destructors of derived classes have unique names. Example:

```
    class Vehicle
    {
        public:
            virtual ~Vehicle();    // all derived class destructors are
                                   // now virtual as well.
    };
```

By declaring a virtual destructor, the above delete operation (`delete vp`) correctly calls `Land`'s destructor, rather than `Vehicle`'s destructor.

Once a destructor is called it performs as usual, whether or not it is a virtual destructor. So, `~Land` first executes its own statements and then calls `~Vehicle`. Thus, the above `delete vp` statement uses late binding to call `~Vehicle` and from this point on the object destruction proceeds as usual.

Destructors should always be defined virtual in classes designed as a base class from which other classes are going to be derived. Often those destructors themselves have no tasks to perform. In these cases the virtual destructor is given an empty body. For example, the definition of `Vehicle::~Vehicle()` may be as simple as:

```
    Vehicle::~Vehicle()
    {
    }
```

Resist the temptation to define virtual destructors (even empty destructors) inline as this complicates class maintenance. Section 14.11 discusses the reason behind this rule of thumb.

# ## 14.3 Pure virtual functions

The base class `Vehicle` is provided with its own concrete implementations of its virtual members (`mass` and `setMass`). However, virtual member functions do not necessarily *have* to be implemented in base classes.

When the implementations of virtual members are omitted from base classes the class imposes requirements upon derived classes. The derived classes are required to provide the 'missing implementations'

This approach, in some languages (like `C#`, `Delphi` and `Java`) known as an *interface*, defines a *protocol*. Derived classes *must* obey the protocol by implementing the as yet not implemented members. If a class contains at least one member whose implementation is missing no objects of that class can be defined.

Such incompletely defined classes are always base classes. They enforce a protocol by merely declaring names, return values and arguments of some of their members. These classes are call *abstract classes* or *abstract base classes*. Derived classes become non-abstract classes by implementing the as yet not implemented members.

Abstract base classes are the foundation of many *design patterns* (cf. *Gamma et al.* (1995)), allowing the programmer to create highly *reusable software*. Some of these design patterns are covered by the *C++ Annotations* (e.g. the *Template Method* in section *23.2*), but for a thorough discussion of design patterns the reader is referred to *Gamma et al.*'s book.

Members that are merely declared in base classes are called *pure virtual functions*. A virtual member becomes a pure virtual member by postfixing `= 0` to its declaration (i.e., by replacing the semicolon ending its declaration by `= 0;`). Example:

```
    #include <iosfwd>
    class Base
```