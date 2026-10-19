# ISO/IEC 14882:2020(E)

(9.3) — for each non-static data member of X that is of class type (or array thereof), the assignment operator selected to copy/move that member is trivial; otherwise the copy/move assignment operator is non-trivial.

10 A copy/move assignment operator for a class X that is defaulted and not defined as deleted is implicitly defined when it is odr-used (6.3) (e.g., when it is selected by overload resolution to assign to an object of its class type), when it is needed for constant evaluation (7.7), or when it is explicitly defaulted after its first declaration. The implicitly-defined copy/move assignment operator is constexpr if

+   (10.1) — X is a literal type, and
+   (10.2) — the assignment operator selected to copy/move each direct base class subobject is a constexpr function, and
+   (10.3) — for each non-static data member of X that is of class type (or array thereof), the assignment operator selected to copy/move that member is a constexpr function.

11 Before the defaulted copy/move assignment operator for a class is implicitly defined, all non-user-provided copy/move assignment operators for its direct base classes and its non-static data members are implicitly defined.
[Note 7: An implicitly-declared copy/move assignment operator has an implied exception specification (14.5). — end note]

12 The implicitly-defined copy/move assignment operator for a non-union class X performs memberwise copy/move assignment of its subobjects. The direct base classes of X are assigned first, in the order of their declaration in the base-specifier-list, and then the immediate non-static data members of X are assigned, in the order in which they were declared in the class definition. Let x be either the parameter of the function or, for the move operator, an xvalue referring to the parameter. Each subobject is assigned in the manner appropriate to its type:

+   (12.1) — if the subobject is of class type, as if by a call to operator= with the subobject as the object expression and the corresponding subobject of x as a single function argument (as if by explicit qualification; that is, ignoring any possible virtual overriding functions in more derived classes);
+   (12.2) — if the subobject is an array, each element is assigned, in the manner appropriate to the element type;
+   (12.3) — if the subobject is of scalar type, the built-in assignment operator is used.

It is unspecified whether subobjects representing virtual base classes are assigned more than once by the implicitly-defined copy/move assignment operator.

> [Example 3:
> struct V { };
> struct A : virtual V { };
> struct B : virtual V { };
> struct C : B, A { };
> It is unspecified whether the virtual base class subobject V is assigned twice by the implicitly-defined copy/move assignment operator for C. — end example]

13 The implicitly-defined copy assignment operator for a union X copies the object representation (6.8) of X. If the source and destination of the assignment are not the same object, then for each object nested within (6.7.2) the object that is the source of the copy, a corresponding object o nested within the destination is created, and the lifetime of o begins before the copy is performed.

# 11.4.7 Destructors [class.dtor]

1 A prospective destructor is introduced by a declaration whose declarator is a function declarator (9.3.4.6) of the form
ptr-declarator ( parameter-declaration-clause ) noexcept-specifieropt attribute-specifier-seqopt
where the ptr-declarator consists solely of an id-expression, an optional attribute-specifier-seq, and optional surrounding parentheses, and the id-expression has one of the following forms:

+   (1.1) — in a member-declaration that belongs to the member-specification of a class or class template but is not a friend declaration (11.9.4), the id-expression is ~class-name and the class-name is the injected-class-name (11.1) of the immediately-enclosing entity or