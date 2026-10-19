*base-specifier* is well-formed because D is derived from A, so checking of *base-specifiers* must be deferred until the entire *base-specifier-list* has been seen. — end example]

8 The names in a default argument (9.3.4.7) are bound at the point of declaration, and access is checked at that point rather than at any points of use of the default argument. Access checking for default arguments in function templates and in member functions of class templates is performed as described in 13.9.2.

9 The names in a default *template-argument* (13.2) have their access checked in the context in which they appear rather than at any points of use of the default *template-argument*.

[Example 3:

```
class B { };
template <class T> class C {
protected:
    typedef T TT;
};

template <class U, class V = typename U::TT>
class D : public U { };

D <C<B> *> d;        // access error, C::TT is protected
```

— end example]

# 11.9.2 Access specifiers [class.access.spec]

1 Member declarations can be labeled by an *access-specifier* (11.7):

```
*access-specifier* : *member-specification*opt
```

An *access-specifier* specifies the access rules for members following it until the end of the class or until another *access-specifier* is encountered.

[Example 1:

```
class X {
    int a;            // X::a is private by default: class used
public:
    int b;            // X::b is public
    int c;            // X::c is public
};
```

— end example]

2 Any number of access specifiers is allowed and no particular order is required.

[Example 2:

```
struct S {
    int a;            // S::a is public by default: struct used
protected:
    int b;            // S::b is protected
private:
    int c;            // S::c is private
public:
    int d;            // S::d is public
};
```

— end example]

3 [Note 1: The effect of access control on the order of allocation of data members is specified in 7.6.9. — end note]

4 When a member is redeclared within its class definition, the access specified at its redeclaration shall be the same as at its initial declaration.

[Example 3:

```
struct S {
    class A;
    enum E : int;
private:
    class A { };        // error: cannot change access
```