bers aren’t too impressive, but the implications of the example are. The process member could implement directory travel, `hello` could define the action to perform when encountering a file. `Base::hello` might simply show the name of a file, but `Derived::hello` might delete the file; might only list its name if its younger than a certain age; might list its name if it contains a certain text; etc., etc. Up to now `Derived` would have to implement process actions itself; Up to now code expecting a `Base` class reference or pointer could only perform `Base`’s actions. Polymorphism allows us to reimplement members of base classes and to use those reimplemented members in code expecting base class references or pointers. Using polymorphism existing code may be reused by derived classes reimplementing the appropriate members of their base classes. It’s about time to uncover how this magic can be realized.

Polymorphism, which is not the default in C++, solves the problem and allows the author of the classes to reach its goal. For the curious reader: prefix `void hello()` in the Base class with the keyword `virtual` and recompile. Running the modified program produces the intended and expected derived `hello`. Why this happens is explained next.

# 14.1  Virtual functions

By default the behavior of a member function called via a pointer or reference is determined by the implementation of that function in the pointer’s or reference’s class. E.g., a `Vehicle *` activates `Vehicle`’s member functions, even when pointing to an object of a derived class. This is known as *early* or *static* binding: the function to call is determined at compile-time. In C++ *late* or *dynamic* binding is realized using *virtual member functions*.

A member function becomes a virtual member function when its declaration starts with the keyword `virtual`. It is stressed once again that in C++, different from several other object oriented languages, this is *not* the default situation. By default *static* binding is used.

Once a function is declared `virtual` in a base class, it remains virtual in all derived classes; even when the keyword `virtual` is not repeated in derived classes.

In the vehicle classification system (see section 13.1) the two member functions `mass` and `setMass` might be declared `virtual`. Concentrating on `mass`, the relevant sections of the class definitions of the class `Vehicle` and `Truck` are shown below. Also, we show the implementations of the member function `mass`:

```
```cpp
class Vehicle
{
    public:
        virtual int mass() const;
};
class Truck: // inherited from Vehicle through Auto and Land
{
    // not altered
};
int Vehicle::mass() const
{
    return d_mass;
}

int Truck::mass() const
{
    return Auto::mass() + d_trailer_wt;
}
```
```

The keyword `virtual` *only* appears in the (Vehicle) base class. There is no need (but there is also no penalty) to repeat it in derived classes. Once a class member has been declared virtual it becomes a virtual member in all derived classes. A member function may be declared `virtual` anywhere in a class hierarchy. The compiler is perfectly happy if `mass` is declared virtual in Auto, rather than