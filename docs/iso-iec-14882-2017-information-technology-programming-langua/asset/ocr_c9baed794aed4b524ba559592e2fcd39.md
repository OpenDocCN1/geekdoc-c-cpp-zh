# ISO/IEC 14882:2017(E)

```
static int b;
};

int X::a = 1;
int X::b = a;

// X::b = X::a
```

— end example — the expression-list in the parenthesized initializer shall be a single expression.

The initialization occurs in the form of *brace-equal-initializer* or condition (9.4), as well as in argument passing, function return, throwing an exception (18.1), handling an exception (18.3), and aggregate member initialization (11.6.1), is called copy-initialization. [Note: Copy-initialization may invoke new [15.8]. — end note]

The initialization occurs in the forms

```
T x(a);
T x{a};
```

as well as in new expressions (8.3.4), static_cast expressions (8.2.9), functional notation type conversion, member-initializers (15.6.2), and the braced-list form of direct-initialization.

The semantics of initializers are: otherwise, the type of the object or reference initialized and the *source* type is the type of the initializer. If the initializer is not a single (possibly parenthesized) expression, the source type is not defined.

+   (17.1) If the initializer is a (non-parenthesized) braced-list or is, the object or reference is list-initialized (11.6.4).

+   (17.2) If the destination is a reference type, see 11.6.3.

+   (17.3) If the destination is any type of characters, an array of char16_t, an array of char32_t, or an array of wchar_t, and the initializer is a literal string, see 11.6.2.

+   (17.4) If the initializer is (), the object is value-initialized.

+   (17.5) Otherwise, if the destination is an array, it is program-initialized.

+   (17.6) If the destination is a type (possibly cv-qualified) class:

+   If the initializer is an expression and the cv-unqualified version of the source type is the class as the class of the destination, the initializer expression is used to initialize the destination object. [Example: x = T(T(T())); calls the T default constructor to initialize x. — example]

+   (16.2) Otherwise, if the destination is direct-initialization, or if it is copy-initialization where the cv-unqualified version of the source type is the same as, or a derived class of, the class, the constructors are chosen through overload resolution (16.3), and the best one is chosen to select and initialize the object, the initializer expression or braced-list is used as its argument. If no constructor applies, the overload resolution is ambiguous, the initialization is ill-formed.

+   (17.3) Otherwise (i.e., for matching copy-initializations), user-defined conversion sequences that can convert the source to the destination type (or when a conversion function is used) a derived class thereof are enumerated as described in 16.3.4, and the best one is chosen through overload resolution (16.3). If the conversion cannot be done or is ambiguous, the initialization is ill-formed. The function selected with the initializer expression as its argument; if the function is a constructor, it is a value of the cv-unqualified version of the destination type whose result object is initialized by the constructor. The call is used to direct-initialize, according

§ 11.6

© ISO/IEC 2017 – All rights reserved 223