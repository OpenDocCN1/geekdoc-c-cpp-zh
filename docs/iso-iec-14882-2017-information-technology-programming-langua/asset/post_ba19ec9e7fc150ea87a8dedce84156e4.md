
# ISO/IEC 14882:2017(E)

(5.3) An id-expression denoting the member in a class access expression (8.2.5) for which the type of the object expression is the current instantiation, and the id-expression, when looked up (6.4.5), refers to at least one member of a class that is the current instantiation or a non-dependent base class thereof.
[Note: If no member is found, and the current instantiation has any non-dependent base class thereof.—end note] The id-expression is a member of an unknown specialization; see below.

```
Example:
template<class T> class A {
    static const int i = 5;
    int n1[]; // refers to a member of the current instantiation
    int n2[]; // A:: refers to a member of the current instantiation
    int n3[A<T>]; // A:: refers to a member of the current instantiation
    int f();
};

template<class T> T A::f() {
    return i;
} // refers to a member of the current instantiation
```
- end example

A name is a dependent member of the current instantiation if it is a member of the current instantiation that, when looked up, refers to at least one member of a class that is the current instantiation.

A name is a member of an unknown specialization if it is:

- (6.1) A qualified-id in which the nested-specifier-name depends a dependent type that is not the current instantiation.
- (6.2) A qualified-id in which the nested-specifier refers to the current instantiation, the current instantiation has at least one dependent base class, and name lookup does not find any member of a class that is the current instantiation or a non-dependent base class thereof.
- (6.3) An id-expression denoting the member in a class access expression (8.2.5) in which the type of the object expression is the current instantiation, the current instantiation has at least one dependent base class, and name lookup of the id-expression does not find a member of a class that is the current instantiation or a non-dependent base class thereof; or
- (6.3.1) the type of the object expression is the current instantiation or it is not the current instantiation.

? If a qualified-id in which the nested-specifier-name refers to the current instantiation is not a member of the current instantiation or a member of an unknown specialization, the program is ill-formed even if the template is instantiated. Similarly, if the id-expression in a class access expression for which the type of the object expression is the current instantiation does not refer to a member of the current instantiation or a member of an unknown specialization, the program is ill-formed if the template containing the member expression is not instantiated; Example:

```
template<class T> class A {
    typedef int type;
    void f() { // OK: refers to a member of the current instantiation
        A<T>::type i; // error: neither a member of the current instantiation nor
        typename A<T>::other j; // a member of an unknown specialization
    }
};
```
- end example

# ISO/IEC 14882:2017(E)

8 If, for a given set of templates, a specialization of a template is instantiated that refers to a member of the current instantiation with a qualified-id or class member expression, the name in the qualified-id or class member access looked up differs from the result of name lookup in the template instantiation context, name lookup is ambiguous.
Example:

```
struct A {
  int m;
};

struct B {
  int m;
};

template<typename T>
struct C : A, T {
  int f() { return this->m; }
  int g() { return m; }
};
```

```
template<int> C::f();
template<int> C::g();
// finds A::m in the template definition context
// finds A::m in the template definition context
// error: finds both A::m and B::m
// OK transformation to class member access syntax
// does not occur in the template definition context; see 17.2.2
```
end example

9 A type is dependent if it:

- (9.1) a template parameter,
- (9.2) a member of an unknown specialization,
- (9.3) a nested class or enumeration that is a dependent member of the current instantiation,
- (9.4) a cv-qualified type where the cv-unqualified type is dependent,
- (9.5) a compound type constructed from any dependent type,
- (9.6) an array whose element type is dependent or bound (any) is value-dependent,
- (9.7) a function type whose specification is value-dependent,
- (9.8) a simple-template-id in which either the template name is a parameter or any of the templates is a dependent argument or an expression that is type-dependent or value-dependent or a pack expression
[Note: This includes an injected-class(Clause 12) of a class template used without a template-argument-list. end note];
- (9.9) denoted by decltype(expression), where expression is type-dependent (17.6.2.2).

[10: Because typedef does not introduce new types, but simply refer to other types, a name that refers to a type that is a member of the current instantiation is dependent only if the type referred to is dependent. end note]

# 17.6.2 Type-dependent expressions

1 Except as described below, an expression is type-dependent if any subexpression is type-dependent.

2 this is type-dependent if the class type of the expression is dependent.

3 an id-expression is type-dependent if it contains:
- (3.1) an identifier identified by name lookup with one more declarations with a dependent type,
- (3.2) an identifier identified by name lookup with one more declarations of the current instantiation that contains a type,
- (3.3) an identifier identified by name lookup with one more declarations with a placeholder type.
- (3.4) an identifier identified by name lookup with one more declarations of member functions that are dependent,
- (3.5) an identifier identified by name lookup with one more declarations whose brace-or-initializer is dependent,
- (3.6) an identifier identified by name lookup with one more declarations where enclosing function is a type, a class template, or a generic lambda;
- (3.7) a template-id that is dependent, or
- (3.8) an identifier identified by name lookup with one more declarations that names a member of an unknown specialization;
- (3.9) a nested-specifier or a qualified-id that names a member of unknown specialization;

or if it refers to a member of the current instantiation and the type of the referenced member is dependent, or the class member access refers to a member of unknown specialization. [Note: For the library macro offset (8.2.5) is type-dependent if the expression of the form x.y or xp->y of the expression is usually the type of the member of the x (or the pointed to by zp). However, if x or xp refer to a dependent type that is not the current instantiation, the type of y is always dependent, or if x or xp refer to a non-dependent type or to the current instantiation, the type of the class member access expression — end note]

- Expressions of the following are type-dependent only if the type specified by the simple-type-specifier or new-type-id is dependent, or if any subsection is type-dependent:
```
simple-type-specifier (expression-list)
::opt new-placement_opt new-type-id
::opt new-placement_opt (type-id) new-initializer_opt
dynamic_cast <type-id> (expression)
static_cast <type-id> (expression)
cast <type-id> (expression)
reinterpret_cast <type-id> (expression)
(type-id) cast-expression
```

- Expressions of the following are never type-dependent (because the type of the expression is dependent):
literal
postfix-expression, pseudo-destructor-name
postfix-expression -> pseudo-destructor-name
sizeof unary-expression
sizeof (type-id)
sizeof ~ (identifier)
alignof (expression)
typeid (type-id)
typeid (type-id)
::opt delete-and-cast-expression
::opt delete-expression_opt
throw assignment-expression_opt
noexcept (expression)
