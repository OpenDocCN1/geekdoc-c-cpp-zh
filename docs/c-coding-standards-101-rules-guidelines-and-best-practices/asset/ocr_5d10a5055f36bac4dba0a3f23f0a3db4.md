# 90. Avoid type switching; prefer polymorphism.

# Summary

Switch off: Avoid switching on the type of an object to customize behavior. Use templates and virtual functions to let types (not their calling code) decide their behavior.

# Discussion

Type switching to customize behavior is brittle, error-prone, unsafe, and a clear sign of attempting to write C or Fortran code in C++. It is a rigid technique that forces you to go back and do surgery on existing code whenever you want to add new features. It is also unsafe because the compiler will not tell you if you forgot to modify all of the switches when you add a type.

Ideally, adding new features to a program equates to adding more new code (see Item 37). In reality, we know that that's not always true—oftentimes, in addition to writing new code, we need to go back and modify some existing code. Changing working code is undesirable and should be minimized, however, for two reasons: First, it might break existing functionality. Second, it doesn't scale well as the system grows and more features are added, because the number of “maintenance knots” that you need to go back and change increases as well. This observation led to the Open-Closed principle that states: An entity (e.g., class or module) should be open for extension but closed for modification. (See [Martin96c] and [Meyer00].)

How can we write code that can be easily extended without modifying it? Use polymorphism by writing code in terms of abstractions (see also Item 36) and then adding various implementations of those abstractions as you add functionality. Templates and virtual function calls form a dependency shield between the code using the abstractions and the code implementing them (see Item 64).

Of course, managing dependencies this way depends on finding the right abstractions. If the abstractions are imperfect, adding new functionality will require changing the interface (not just adding new implementations of the interface), which usually requires changes to existing code. But abstractions are called “abstractions” for a reason—they are supposed to be much more stable than the “details,” that is, the abstractions’ possible implementations.

Contrast that with code that uses few or no abstractions, but instead traffics directly in concrete types and their specific operations. That code is “detailed” already—in fact, it is swimming in a sea of details, a sea in which it is doomed soon to drown.

# Examples

*Example: Drawing shapes.* The classic example is drawing objects. A typical C-style, switch-on-type solution would define an enumerated member variable `id_` for each