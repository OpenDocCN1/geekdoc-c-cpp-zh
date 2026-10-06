ISO/IEC 14882:2017(E)

# Special member functions [special]

The default constructor (15.1), copy constructor and copy assignment operator (15.8), move constructor and move assignment operator (15.8), and destructor (15.4) are special member functions.[Note: The implementation will implicitly declare these member functions for some class types when the program does not explicitly declare them. The implementation will implicitly define them if they are odr-declared (6.2). See 15.1.4 and 15.8.—end note.] An implicitly-declared special member function is declared at the closing ) of the decl-specifier. Programs shall not implicitly-declared special member functions.

Programs may explicitly refer to implicitly-declared special member functions.[Example: A program may explicitly call, take the address of, or a pointer to an implicitly-declared special member function.]

```
struct A {
    // implicitly-declared :operator=
struct B {
    B&operator=(const B&);
};
B B::operator=(const B& s) {
    this->operator(s); // well formed
    return *this;
    }
};
// end example
```

+   3 [Note: The special member functions affect the ways objects of class type are created, copied, moved and destroyed, and how such special member functions can be converted to values of other types. Often such special member functions are implicitly called.—end note.]

+   4 Special member functions obey the usual access rules (Clause 14).[Example: Declaring a constructor ensures that only non-abstract derived classes and classes can create objects using.—end example]

+   5 For a class, its non-static data members, its non-virtual base classes, and if the class is not abstract (13.4), its base classes are all potentially constructed subobjects. [class.ctor]

# 15.1 Constructors [class.ctor]

+   1 Constructors do not have names. In a declaration of a constructor, the declarator is a function declaration-(11.5.3) of the form
ptr-declarator (parameter-declarator-clause) noexcept-specifier_opt attribute-specifier-seq_opt
where the ptr-declarator consists of an id-expression, an optional attribute-specifier, and optional surrounding parentheses, and the id-expression has one of the following:

+   (1.1) in a member declaration that belongs to the member-specification of a class but not a friend declaration (14.3), the id-expression is the injected-class-name (Clause 12) of the immediately-closing class;

+   (1.2) in a member declaration that belongs to the member-specification of a class but not a friend declaration, the id-expression is a class-name that names the current instantiation (17.6.2.1) of the immediately-closing class template; or

+   (1.3) in a declaration in namespace scope or in a friend declaration, the id-expression is a qualified-id that names a constructor (6.4.3.1).

The class-name shall not be a type-name. In a constructor declaration, each decl-specifier in the optional

§ 15.1 ISO/IEC 2017 - All rights reserved 278