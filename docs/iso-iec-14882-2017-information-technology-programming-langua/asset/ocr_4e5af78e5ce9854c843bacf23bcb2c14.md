# ISO/IEC 14882:2017(E)

Here, x.i is initialized with 99, x.f is initialized with 88.8, and complex::complex(double) is called for the initialization of x.c. [Note: Braces are elided in the initializer-list for any aggregate, even if the aggregate has members of a class with user-defined type conversions; see 16.6.1.]

[Note: If T is a class with no default constructor, any declaration of an object of T (or array) is ill-formed if initialization is specified (see 15.6 and 11.6.)]

[Note: The order in which with static or storage duration initialization is described in 66.6.3 and 9.7.]

# 15.6.2 Initializing bases and members [class.base.init]

In the definition of a constructor for a class, initializers for direct and virtual base class subobjects and non-static data members can be specified by a ctor-initializer, which has the form

```
ctor-initializer:
  : mem-initializer-list
  mem-initializer-list:
    mem-initializer ...opt
    mem-initializer-list, mem-initializer ...opt
mem-initializer:
  mem-initializer(expression_list)opt
  mem-initializer(braced-init)
  class-identifier:
    identifier
class-orclinetype
```

In a member initializer an unqualified identifier is looked up in the scope of the constructor's class, and not found in such class, it is looked up in the scope containing the constructor's definition. [Note: If the class contains a member with the same name as a direct or virtual base class of the class, a member-initializer naming the member or base composed of a single identifier refers to the constructor's class, a non-static data member of the constructor's class. A member-initializer for the hidden base may be specified using a qualified name.—end note] Unless the member-initializer names the data member of the constructor's class, a direct or virtual base of that class, the member-initializer is ill-formed.

A member-initializer can initialize a base class using any class-or-decltype that denotes that base class type. [Example:]

```
struct A {
  A global_A;
};
struct B {
};
struct C : public A, public B {C};
  C() : A(global_A) {} // member-initializer for base A
—[end example]
```

A member-initializer is ambiguous because it denotes a direct virtual base class and an inherited virtual base class, the member-initializer is ill-formed. [Example:]

```
struct A {
  A();
};
struct B : virtual A {
};
struct C : public A, public B {
};
  C() : A() {} // ill-formed: which A?
—[end example]
```

A ctor-initializer may initialize a variant of the constructor's class. If a ctor-initializer specifies more than one member-initializer for the same member or for the same base class, the ctor-initializer is ill-formed.

§15.6.2 ©ISO/IEC 2017 - All rights reserved 292