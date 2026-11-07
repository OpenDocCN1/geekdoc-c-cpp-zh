opposite direction (base to derived) is possible only if the derived class defines a conversion operator, which is a constructor that has a reference to the base type as its sole argument, or else defines an assignment operator with a base-class parameter.

+   10. It can do so because C++ allows a reference to a base type to refer to any type derived from that base.

+   11. Passing an object by value invokes the copy constructor. Because the formal argument is a base-class object, the base-class copy constructor is invoked. The copy constructor has as its argument a reference to the base class, and this reference can refer to the derived object passed as an argument. The net result is that a new base-class object whose members correspond to the base class portion of the derived object is produced.

+   12. Passing an object by reference instead of by value enables the function to avail itself of virtual functions. Also passing an object by reference instead of by value may use less memory and time, particularly for large objects. The main advantage of passing by value is that it protects the original data, but you can accomplish the same end by passing the reference as a const type.

+   13. If `head()` is a regular method, then `ph->head()` invokes `Corporation::head()`. If `head()` is a virtual function, then `ph->head()` invokes `PublicCorporation::head()`.

+   14. First, the situation does not fit the `is-a` model, so public inheritance is not appropriate. Second, the definition of `area()` in `House` hides the `Kitchen` version of `area()` because the two methods have different signatures.

# # Answers to Chapter Review for Chapter 14

| | | |
|---|---|---|
| 1. class Bear | class PolarBear | Public; a polar bear is a kind of bear |
| class Kitchen | class Home | Private; a home has a kitchen |
| class Person | class Programmer | Public; a programmer is a kind of person |
| class Person | class HorseAndJockey | Private; a horse and jockey team contains a person |
| class Person, class Automobile | class Driver | Person public because a driver is a person; Automobile private because a driver has an automobile |