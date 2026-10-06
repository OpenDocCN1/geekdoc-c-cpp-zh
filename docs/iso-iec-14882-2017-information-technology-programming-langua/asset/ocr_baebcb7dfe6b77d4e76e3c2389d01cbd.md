# ISO/IEC 14882:2017(E)

(10.2) a potentially constructed subobject M (or array thereof) cannot be copied/moved because overload resolution (16.3), as applied to M's corresponding constructor, results in an ambiguity or a function that is deleted or inaccessible from the default constructor,

(10.3) any potentially constructed subobject of a destructor that is deleted or inaccessible from the default constructor,

(10.4) for the copy constructor, a non-static data member of value reference type.

A moved constructor that is defined as deleted is ignored by overload resolution (16.3, 16.4). [Note: A moved constructor would otherwise interfere with initialization from an rvalue which can use the copy constructor. — end note]

+   11 A copy constructor for class X is used if it is not user-deleted and if:

+   (11.1) class has no virtual functions (13.3) and no base classes (13.1), and

+   (11.2) the selected copy/move each base class subobject is trivial, and for each non-static data member of X that is of class type (or array), the selected copy/move each member is trivial;

otherwise the copy/move constructor is non-trivial.

+   12 A move constructor that is defined and not defined as deleted is implicitly defined if it is used (6.2) or if it is explicitly defined after its first declaration. [Note: The copy/move constructor is implicitly defined if the explicit defines its rvalue (6.2, 15.2). — Note: If the implicitly-defined constructor satisfies the requirements of a constexpr (10.1.5), the implicitly-defined constructor is constexpr.

+   13 Before the copy constructor for class X is defined, all potentially subobjects have been implicitly defined. [Note: An implicitly-deleted copy/move constructor for a non-class X performs a copy/move of its bases and members. [Note: Default initializer of non-static data members are ignored. See the example in 15.6.2.] — The order of initialization is the same as the order of bases in a user-defined class, except for non-static members (15.6.3). Let either be the parameter of the constructor or, for the move constructor, an rvalue reference to that parameter. Each base or non-static data member is copied/moved in the manner appropriate to its type:

+   (14.1) if the member is an array, each element is direct-initialized with the corresponding subobject of X;

+   (14.2) if a member has reference type T&, it is direct-initialized with the corresponding member of X;

+   (14.3) otherwise, the base or member is initialized with the corresponding implicitly-defined copy/move constructor (see 15.6.2).

Virtual base class subclasses shall be initialized only once by the implicitly-defined copy/move constructor

15 The implicitly-defined copy/move constructor for a union X copies the object type (6.9) of X.

# 15.8.2 copy/move assignment operator

```
[class.assign]
```

1 A user-declared copy assignment operator X::operator= is a non-template member function of class X with one parameter of type X, const X&, or const X&&. [Note: An overloaded assignment operator must be declared with only one parameter; see 16.5. — end note] [Note: More than one assignment operator may be defined for a class. — end note] [If

120) A template assignment operator or an assignment operator taking a reference parameter is not allowed to suppress the implicit declaration of a copy assignment operator. Such assignment operator is considered in conflict resolution with other assignment operators, and, if selected, will be used to assign an object.