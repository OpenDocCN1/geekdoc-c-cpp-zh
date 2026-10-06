# ISO/IEC 14882:2017(E)

A destructor is used to destroy objects of its class. The address of a destructor shall not be taken. A destructor can be invoked for a const, volatile or const volatile object. const and volatile semantics (10.1.7.1) are not applied to an object destruction. They stop being effective when in the destructor for the most derived object (4.5).

> > [Note: A declaration of a destructor that does not have a noexcept-specifier has the same exception specification as it had been implicitly declared (18.4). — end]

If a class has no user-declared destructor, a destructor is implicitly declared as defaulted (11.4). An implicitly-declared destructor is an inline member of its class.

A defaulted destructor for a class X is defined as:

+   (5.1) X is an inline-like class that has a member with a non-virtual destructor,

+   (5.2) any potentially constructed subobject has type M (or array thereof) and M has a deleted destructor or a destructor that is inaccessible from the defaulted destructor,

+   (5.3) or, for a virtual destructor, lookup of the non-deallocation function fails in an ambiguity or a function that is declared or inaccessible from the defaulted destructor.

A destructor is virtual if it is not user-provided and if

+   (6.1) all of the base classes of class X have virtual destructors and,

+   (6.2) for all the non-static data members of class X are of type const (or array thereof), each such class has a virtual destructor.

Otherwise, the destructor is non-virtual.

A destructor that is defined and not deleted is implicitly defined when it is not odr-used (6.2) or when it is explicitly defined after its first declaration.

Before the destructor of a class is implicitly defined, all the non-user-provided destructors for its base classes and non-static data members have been implicitly defined.

After the body of the destructor and after destroying any automatic objects located within the body, a destructor for class X executes the destructors for Y non-virtual base classes, the destructors for X's non-virtual derived base classes, and if X is the type of the most derived class (15.6.2), its destructor qualified name, that is, ignoring any potential virtual overriding destructors in more derived classes. The destructors for X's virtual base classes. Bases and members are destroyed in the reverse order of the completion of their constructor (15.5.2). A return statement in a destructor must not return to the caller; before transferring control to the caller the destructor, all destructors for elements of an array are executed in order of their construction (15.6).

A destructor can be declared virtual (13.3) or pure virtual (13.4); if objects of class or any derived class are created in particular, the destructor shall be defined. If a class has a virtual destructor, its destructor (whether user- or implicitly-declared) is virtual.

> > [Note: Some languages have special semantics used during destruction: is 15.7.— end note]

A destructor is invoked implicitly

+   (12.1) — for a constructed object with static storage duration (6.7.1) at program termination (6.6.4),

+   (12.2) — for a constructed object with thread storage duration (6.7.2) at thread exit,

+   (12.3) — for a constructed object with automatic storage duration (6.7.3) when the block in which an object is created exits (9.7).

§ ISO/IEC 2017 — All rights reserved 287