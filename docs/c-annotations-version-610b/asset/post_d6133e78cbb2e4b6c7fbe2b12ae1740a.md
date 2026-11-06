
- classes:

```cpp
class Derived1: virtual public Base
class Derived2: virtual public Base
```

Both base classes use virtual derivation and so only one `Base` class object will be present in the `Final` class object. The following constructors are called in the order shown:

```
Base,
Derived1,
Derived2
```

Virtual derivation is, in contrast to virtual functions, a pure compile-time issue. Virtual inheritance merely defines how the compiler defines a class’s data organization and construction process.

### 14.5.3 When virtual derivation is not appropriate

Virtual inheritance can be used to merge multiply occurring base classes. However, situations may be encountered where multiple occurrences of base classes is appropriate. Consider the definition of a `Truck` (cf. section 13.5):

```cpp
class Truck: public Auto
{
    int d_trailer_mass;

public:
    Truck();
    Truck(int engine_mass, int sp, char const *nm,
          int trailer_mass);

    void setMass(int engine_mass, int trailer_mass);
    int mass() const;
};
Truck::Truck(int engine_mass, int sp, char const *nm,
             int trailer_mass)
:
    Auto(engine_mass, sp, nm)
{
    d_trailer_mass = trailer_mass;
}
int Truck::mass() const
{
    return                  // sum of:
        Auto::mass() +      // engine part plus
        d_trailer_mass;     // the trailer
}
```

This definition shows how a `Truck` object is constructed to contain two mass fields: one via its derivation from `Auto` and one via its own `int d_trailer_mass` data member. Such a definition is of course valid, but it could also be rewritten. We could derive a `Truck` from an `Auto` and from a `Vehicle`, thereby explicitly requesting the double presence of a `Vehicle`; one for the mass of the engine and cabin, and one for the mass of the trailer. A slight complication is that a class organization like `class Truck: public Auto, public Vehicle` is not accepted by the C++ compiler. As a `Vehicle` is already part of an `Auto`, it is therefore not needed once again. This organization may, however, be forced using a small trick. By creating an additional class inheriting from `Vehicle` and deriving `Truck` from that additional class rather than directly from `Vehicle`, the problem is solved. Simply derive a class `TrailerVeh` from `Vehicle`, and then `Truck` from `Auto` and `TrailerVeh`:

```cpp
class TrailerVeh: public Vehicle
{
    public:
        TrailerVeh(int mass)
        :
            Vehicle(mass)
            {}
};
class Truck: public Auto, public TrailerVeh
{
    public:
        Truck();
        Truck(int engine_mass, int sp, char const *nm, int trailer_mass);
        void setMass(int engine_mass, int trailer_mass);
        int mass() const;
};
inline Truck::Truck(int engine_mass, int sp, char const *nm,
                    int trailer_mass)
:
    Auto(engine_mass, sp, nm),
    TrailerVeh(trailer_mass)
{}
inline int Truck::mass() const
{
    return                         // sum of:
        Auto::mass() +             // engine part plus
        TrailerVeh::mass();        // the trailer
}
```

## 14.6 Run-time type identification

**C++** offers two ways to (run-time) retrieve the type of objects and expressions. The possibilities of C++’s run-time type identification are limited compared to languages like **Java**. Usually static type checking and static type identification is used in **C++**. Static type checking is possibly safer and certainly more efficient than run-time type identification and should therefore be preferred over run-time type identification. But situations exist where run-time type identification is appropriate. C++ offers run-time type identification through the *dynamic cast* and *typeid* operators.

- A `dynamic_cast` is used to convert a base class pointer or reference to a derived class pointer or reference. This is also known as *down-casting*.
- The `typeid` operator returns the actual type of an expression.

These operators can be used with objects of classes having at least one virtual member function.

### 14.6.1 The dynamic_cast operator

The `dynamic_cast<>` operator is used to convert a base class pointer or reference to, respectively, a derived class pointer or reference. This is also called *down-casting* as the direction of the cast is *down* the inheritance tree.

A dynamic cast is performed at run-time. A prerequisite for using a dynamic cast is the existence of at least one virtual member function in the base class.

In the following example a pointer to the class `Derived` is obtained from the `Base` class pointer `bp`:

```cpp
class Base
{
    public:
        virtual ~Base();
};
class Derived: public Base
{
    public:
        char const *toString();
};
inline char const *Derived::toString()
{
    return "Derived object";
}
int main()
{
    Base *bp;
    Derived *dp;
    Derived d;

    bp = &d;

    dp = dynamic_cast<Derived *>(bp);

    if (dp)
        cout << dp->toString() << '\n';
    else
        cout << "dynamic cast conversion failed\n";
}
```

In the condition of the above `if` statement the success of the dynamic cast is verified. This verification must be performed at *run-time*, as the actual class of the objects to which the pointer points is only known then. If a base class pointer is provided, the dynamic cast operator returns 0 on failure and a pointer to the requested derived class on success.

Assume a `vector<Base *>` is used. Such a vector’s pointers may point to objects of various classes, all derived from `Base`. A dynamic cast returns a pointer to the specified class if the base class pointer indeed points to an object of the specified class and returns 0 otherwise. So we could determine the actual class of an object a pointer points to by performing a series of checks to find the actual derived class to which a base class pointer points. Example:

```cpp
class Base
{
    public:
        virtual ~Base();
};
class Derived1: public Base;
class Derived2: public Base;

int main()
{
    vector<Base *> vb(initializeBase());

    Base *bp = vb.front();

    if (dynamic_cast<Derived1 *>(bp))
        cout << "bp points to a Derived1 class object\n";
    else if (dynamic_cast<Derived2 *>(bp))
        cout << "bp points to a Derived2 class object\n";
}
```

Alternatively, a reference to a base class object may be available. In this case the `dynamic_cast` operator throws an exception if the down-casting fails. Example:

```cpp
#include <iostream>
#include <typeinfo>

class Base
{
    public:
        virtual ~Base();
        virtual char const *toString();
};
inline char const *Base::toString()
{
    return "Base::toString() called";
}
class Derived1: public Base
{};
class Derived2: public Base
{};

Base::~Base()
{}
void process(Base &b)
{
    try
    {
        std::cout << dynamic_cast<Derived1 &>(b).toString() << '\n';
    }
    catch (std::bad_cast)
    {}
    try
    {
        std::cout << dynamic_cast<Derived2 &>(b).toString() << '\n';
    }
    catch (std::bad_cast)
    {
        std::cout << "Bad cast to Derived2\n";
    }
}
int main()
{
    Derived1 d;
    process(d);
}
/*
    Generated output:

    Base::toString() called
    Bad cast to Derived2
*/
```

In this example the value `std::bad_cast` is used. A `std::bad_cast` exception is thrown if the dynamic cast of a reference to a derived class object fails.

Note the form of the catch clause: `bad_cast` is the name of a type. Section 17.4.1 describes how such a type can be defined.

The dynamic cast operator is a useful tool when an existing base class cannot or should not be modified (e.g., when the sources are not available), and a derived class may be modified instead. Code receiving a base class pointer or reference may then perform a dynamic cast to the derived class to access the derived class’s functionality.

One may wonder what the difference is between a `dynamic_cast` and a `reinterpret_cast`. One of the differences is of course that the `dynamic_cast` can operate on references while the `reinterpret_cast` can only operate on pointers. But is there a difference when both arguments are pointers?

When the `reinterpret_cast` is used, we tell the compiler that it literally should re-interpret a block of memory as something else. A `reinterpret_cast` could be used to access the individual bytes of an `int`. An `int` consists of `sizeof (int)` bytes, and these bytes can be accessed by reinterpreting the location of the `int` value as a `char *`. When using a `reinterpret_cast` the compiler can no longer offer safeguards against stupidity. The compiler will happily `reinterpret_cast` an `int *` to a `double *`, but the resulting dereference produces at the very least a questionable value.

The `dynamic_cast` also reinterprets a block of memory, but here a run-time safeguard is provided. The `dynamic_cast` fails when the requested type doesn’t match the actual type of the object we’re pointing at. The `dynamic_cast`’s purpose is also much more restricted than the `reinterpret_cast`’s purpose, as it can only be used for downcasting to derived classes having virtual members.

In the end a dynamic cast is a cast, and casts should be avoided. When the need for dynamic casting arises, ask yourself whether the base class has appropriately been designed. In situations where code expects a base class reference or pointer, the base class interface should be all that is required and using a dynamic cast should not be necessary. Maybe the base class’s virtual interface can be modified so as to prevent the use of dynamic casts. Start frowning when encountering code using dynamic casts. When using dynamic casts in your own code, always properly document why the dynamic cast was appropriately used and could not have been avoided.

### 14.6.2 The `typeid` operator

As with the `dynamic_cast` operator, `typeid` is usually applied to references to base class objects that refer to derived class objects. `typeid` should only be used with base classes offering virtual members. Before using `typeid`, the `<typeinfo>` header file must have been included.

The `typeid` operator returns an object of type `type_info`. Different compilers may offer different implementations of the class `type_info`, but at the very least `typeid` must offer the following interface:

```cpp
class type_info
{
    public:
        virtual ~type_info();
        int operator==(type_info const &other) const;
        int operator!=(type_info const &other) const;
        bool before(type_info const &rhs) const;
        char const *name() const;
    private:
        type_info(type_info const &other);
        type_info &operator=(type_info const &other);
};
```

Note that this class has a private copy constructor and a private overloaded assignment operator. This prevents code from constructing `type_info` objects and prevents code from assigning `type_info` objects to each other. Instead, `type_info` objects are constructed and returned by the `typeid` operator.
