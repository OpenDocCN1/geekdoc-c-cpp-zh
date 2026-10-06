# ISO/IEC 14882:2017(E)

decl-specifier-seq shall be friend, inline, explicit, or constexpr. [Example:

```
struct S {
    S(); // declares the constructor
};
::S() { // defines the constructor
 // end example
```

2 A constructor is used to initialize objects of its class type. never found during lookup; however an explicit type conversion using the functional notation (8.2.3) will cause a constructor to be initialized at order. [Note: For initialization of class type see 12.8 and note]

3 A constructor can be invoked for a const, volatile or const volatile object. const and volatile semantics (10.7.1) are never applied on an object. They come into when the constructor for the most derived object (4.5) ends.

4 A default constructor for a class X for which each parameter is not a function parameter has a default argument (including the case of a constructor with no parameters). If there is no user-declared constructor for class X, a non-explicit constructor having no parameters is implicitly declared as defaulted (11.4). It is an inline public member of its class.

5 A deleted default constructor for class X is defined as follows:

+   (5.1) X is a union that has a variant member with a non-trivial default constructor and no variant member of X has a default member

+   (5.2) X is a union that has a variant member with a non-trivial default constructor and no variant member of the anonymous union has a default member initializer,

+   (5.3) any non-static data member of class-qualified (12.2) is of reference type,

+   (5.4) any non-static data member of class-qualified type (or array thereof) with no brace-or-initializer is not a user-provided default constructor,

+   (5.5) X is a union and all of its variant members are of const-qualified type (or array thereof),

+   (5.6) X is a union and all of its anonymous member are of const-qualified type (or array thereof), has potentially deleted brace-or-overload-initializer, class type M (or array thereof) and either M has no default constructor or overload resolution (16.3) as applied to M’s corresponding result in an ambiguity or in a function that is deleted or inaccessible from the default constructor,

+   (5.7) any potentially deleted subobject has a destructor that is deleted or inaccessible from the default constructor.

6 A default constructor is trivial if it is not user-provided and if:

+   (6.1) its class has no virtual functions (13.3) and no virtual base classes (13.1), and

+   (6.2) no non-static data member of its class has a default member initializer (12.2), and

+   (6.3) all the direct base members of its class have trivial default constructors, and

+   (6.4) for all the non-static data members of its class are of class type (or array thereof), each such class has a trivial default constructor.

Otherwise, the default constructor is non-trivial.

7 A default constructor that is deleted and not defined is implicitly defined when it is odrused (6.2)