Otherwise, the implicitly-declared copy assignment operator will have the form
```
X& X::operator=(X&)
```

3 A user-declared move assignment operator X::operator= is a non-static non-template member function of class X with exactly one parameter of type X&&, const X&&, volatile X&&, or const volatile X&&.

> [Note 4: An overloaded assignment operator must be declared to have only one parameter; see 12.6.3.2. — end note]

> [Note 5: More than one form of move assignment operator can be declared for a class. — end note]

4 If the definition of a class X does not explicitly declare a move assignment operator, one will be implicitly declared as defaulted if and only if

+   (4.1) — X does not have a user-declared copy constructor,
+   (4.2) — X does not have a user-declared move constructor,
+   (4.3) — X does not have a user-declared copy assignment operator, and
+   (4.4) — X does not have a user-declared destructor.

> [Example 2: The class definition
> ```
> struct S {
>   int a;
>   S& operator=(const S&) = default;
> };
> ```
> will not have a default move assignment operator implicitly declared because the copy assignment operator has been user-declared. The move assignment operator may be explicitly defaulted.
> ```
> struct S {
>   int a;
>   S& operator=(const S&) = default;
>   S& operator=(S&&) = default;
> };
> ```
> — end example]

5 The implicitly-declared move assignment operator for a class X will have the form
```
X& X::operator=(X&&)
```

6 The implicitly-declared copy/move assignment operator for class X has the return type X&; it returns the object for which the assignment operator is invoked, that is, the object assigned to. An implicitly-declared copy/move assignment operator is an inline public member of its class.

7 A defaulted copy/move assignment operator for class X is defined as deleted if X has:

+   (7.1) — a variant member with a non-trivial corresponding assignment operator and X is a union-like class, or
+   (7.2) — a non-static data member of const non-class type (or array thereof), or
+   (7.3) — a non-static data member of reference type, or
+   (7.4) — a direct non-static data member of class type M (or array thereof) or a direct base class M that cannot be copied/moved because overload resolution (12.4), as applied to find M's corresponding assignment operator, results in an ambiguity or a function that is deleted or inaccessible from the defaulted assignment operator.

> [Note 6: A defaulted move assignment operator that is defined as deleted is ignored by overload resolution (12.4, 12.5). — end note]

8 Because a copy/move assignment operator is implicitly declared for a class if not declared by the user, a base class copy/move assignment operator is always hidden by the corresponding assignment operator of a derived class (12.6.3.2). A using-declaration (9.9) that brings in from a base class an assignment operator with a parameter type that can be that of a copy/move assignment operator for the derived class is not considered an explicit declaration of such an operator and does not suppress the implicit declaration of the derived class operator; the operator introduced by the using-declaration is hidden by the implicitly-declared operator in the derived class.

9 A copy/move assignment operator for class X is trivial if it is not user-provided and if:

+   (9.1) — class X has no virtual functions (11.7.3) and no virtual base classes (11.7.2), and
+   (9.2) — the assignment operator selected to copy/move each direct base class subobject is trivial, and