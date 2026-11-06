
The destructor of the class pointed to by `bp` is going to be called when `delete bp` is executed. Thus, late binding is realized for destructors even though the destructors of derived classes have unique names. Example:

```cpp
class Vehicle
{
    public:
        virtual ~Vehicle();    // all derived class destructors are
                               // now virtual as well.
};
```

By declaring a virtual destructor, the above delete operation (`delete vp`) correctly calls `Land`'s destructor, rather than `Vehicle`'s destructor.

Once a destructor is called, it performs as usual, whether or not it is a virtual destructor. So, `~Land` first executes its own statements and then calls `~Vehicle`. Thus, the above `delete vp` statement uses late binding to call `~Land` and from this point on, the object destruction proceeds as usual.

Destructors should always be defined virtual in classes designed as a base class from which other classes are going to be derived. Often those destructors themselves have no tasks to perform. In these cases the virtual destructor is given an empty body. For example, the definition of `Vehicle::~Vehicle()` may be as simple as:

```cpp
Vehicle::~Vehicle()
{
}
```

Resist the temptation to define virtual destructors (even empty destructors) inline as this complicates class maintenance. Section 14.11 discusses the reason behind this rule of thumb.

## 14.3 Pure virtual functions

The base class `Vehicle` is provided with its own concrete implementations of its virtual members (`mass` and `setMass`). However, virtual member functions do not necessarily *have* to be implemented in base classes.

When the implementations of virtual members are omitted from base classes, the class imposes requirements upon derived classes. The derived classes are required to provide the 'missing implementations'.

This approach, in some languages (like `C#`, `Delphi` and `Java`) known as an *interface*, defines a *protocol*. Derived classes *must* obey the protocol by implementing the as yet not implemented members. If a class contains at least one member whose implementation is missing, no objects of that class can be defined.

Such incompletely defined classes are always base classes. They enforce a protocol by merely declaring names, return values and arguments of some of their members. These classes are called *abstract classes* or *abstract base classes*. Derived classes become non-abstract classes by implementing the as yet not implemented members.

Abstract base classes are the foundation of many *design patterns* (cf. *Gamma et al.* (1995)), allowing the programmer to create highly *reusable software*. Some of these design patterns are covered by the *C++ Annotations* (e.g. the *Template Method* in section *23.2*), but for a thorough discussion of design patterns the reader is referred to *Gamma et al.*'s book.

Members that are merely declared in base classes are called *pure virtual functions*. A virtual member becomes a pure virtual member by postfixing `= 0` to its declaration (i.e., by replacing the semicolon ending its declaration by `= 0;`). Example:

```cpp
#include <iosfwd>
class Base
{
    public:
        virtual ~Base();
        virtual std::ostream & insertInto(std::ostream &out) const = 0;
};
inline std::ostream &operator<<(std::ostream &out, Base const &base)
{
    return base.insertInto(out);
}
```

All classes derived from `Base` *must* implement the `insertInto` member function, or their objects cannot be constructed. This is neat: all objects of class types derived from `Base` can now always be inserted into `ostream` objects.

Could the virtual destructor of a base class ever be a pure virtual function? The answer to this question is no. First of all, there is no need to enforce the availability of destructors in derived classes as destructors are provided by default (unless a destructor is declared with the `= delete` attribute using the new C++11 standard). Second, if it is a pure virtual member its implementation does not exist. However, derived class destructors eventually call their base class destructors. How could they call base class destructors if their implementations are lacking? More about this in the next section.

Often, but not necessarily, pure virtual member functions are `const` member functions. This allows the construction of constant derived class objects. In other situations this might not be necessary (or realistic), and non-constant member functions might be required. The general rule for `const` member functions also applies to pure virtual functions: if the member function alters the object’s data members, it cannot be a `const` member function.

Abstract base classes frequently don’t have data members. However, once a base class declares a pure virtual member it *must* be declared identically in derived classes. If the implementation of a pure virtual function in a derived class alters the derived class object’s data, then *that* function cannot be declared as a `const` member. Therefore, the author of an abstract base class should carefully consider whether a pure virtual member function should be a `const` member function or not.

### 14.3.1 Implementing pure virtual functions

Pure virtual member functions may be implemented. To implement a pure virtual member function, provide it with its normal `= 0;` specification, but implement it as well. Since the `= 0;` ends in a semicolon, the pure virtual member is always at most a declaration in its class, but an implementation may either be provided outside of its interface (maybe using `inline`).

Pure virtual member functions may be called from derived class objects or from its class or derived class members by specifying the base class and scope resolution operator together with the member to be called. Example:

```cpp
#include <iostream>

class Base
{
    public:
        virtual ~Base();
        virtual void pureimp() = 0;
};
Base::~Base()
{}
void Base::pureimp()
{
    std::cout << "Base::pureimp() called\n";
}
```

Outside of this context, they are just plain identifiers, allowing the programmer to define a variable like `bool final`.

The identifier `final` can be applied to class declarations to indicate that the class cannot be used as a base class. E.g.:

```cpp
class Base1 final              // cannot be a base class
{};
class Derived1: public Base1   // ERR: Base1 is final
{};

class Base2                       // OK as base class
{};
class Derived2 final: public Base2 // OK, but Derived2 can’t be
{};                                // used as a base class
class Derived: public Derived2     // ERR: Derived2 is final
{};
```

The identifier `final` can also be added to virtual member declarations. This indicates that those virtual members cannot be overridden by derived classes. The restricted polymorphic character of a class, mentioned above, can thus be realized as follows:

```cpp
class Base
{
    virtual int v_process();    // define polymorphic behavior
    virtual int v_call();
    virtual int v_display();
};
class Derived: public Base     // Derived restricts polymorphism
{                               // to v_call and v_display
    virtual int v_process() final;
};
class Derived2: public Derived
{
    // int v_process();          No go: Derived::v_process is final
    virtual int v_display();    // OK to override
};
```

To allow the compiler to detect typos, differences in parameter types, or differences in member function modifiers (e.g., const vs. non-const), the identifier `override` can (should) be appended to derived class members overriding base class members. E.g.,

```cpp
class Base
{
    virtual int v_process();
    virtual int v_call() const;
    virtual int v_display(std::ostream &out);
};
class Derived: public Base
{
    virtual int v_proces() override;       // ERR: v_proces != v_process
    virtual int v_call() override;          // ERR: not const
                                           // ERR: parameter types differ
    virtual int v_display(std::ostream &out) override;
};
```
