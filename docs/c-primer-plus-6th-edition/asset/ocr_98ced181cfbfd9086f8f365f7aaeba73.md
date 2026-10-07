# Summary

and protected members of the base class become private members of the derived class.
With protected inheritance, public and protected members of the base class become pro-
cted of the derived class.Thus, in either case, the public interface of the base
class becomes an internal interface for the derived class.This is sometimes described as
heriting the implementation but not the interface because a derived object can explic-
ity the base-class interface.Thus, you can not view a derived object as a kind of base
object. Because of this, a base-class pointer or reference is not allowed to refer to a
derived object without an explicit type cast.
You can also reuse code by developing a class with members that are themselves
objects. This approach, called containment, layering, or composition, also models the has-rela
ship.so it is usually preferred. However, private and protected inheritance have slightly
different capabilities. For example, inheritance allows a derived class to access protected
members of a base class. It also allows a derived class to refine a virtual function inher-
ited the base class. Because containment is not a form of inheritance, neither of
these capabilities are options when you reuse code via containment. On the other
hand, containment is more suitable if you need several objects of a given class. For example-
a, state class could contain any array of Country.
Multiple inheritance (MI) allows you to reuse code for more than one class in a class
design. Private or protected MI can create problems with multidef names and multi-inherited
bases.You can use class qualifiers to resolve name ambiguities and virtual base classes to
avoid multi-inherited bases. However, using virtual base introduces new rules for
writing initialization lists for constructors and for resolving ambiguities.
Class templates allow you to generate a generic class design in which a type, usually a member
type, is represented by a type parameter. A typical template looks like this:

```
template <class T>
class Ic {
    T v;
public:
    Ic(const T& val) : v(val) { }
};

```

Here T is the type parameter, and it acts as a stand-in for a real type to be specified at
later time. (This parameter can have any valid C++ name, but T and Type are common
choices.)You can also use typename instead of class in this context:

```
template <typename T> // same as template <class T>
class Rev { ... };
```

Class definitions (instantiations) are generated when you declare a class object and
specific a particular type. For example, the following declaration causes the compiler to