
# ISO/IEC 14882:2017(E)

function definition shall not be an incomplete (possibly cv-qualified) class type in the context of the function definition unless the function is defined (11.4.3).

A typedef function type may be used to declare a function but shall not be used to define a function (11.4).
Example:

```
typedef void F();
F() {      // OK: equivalent to void F();
F() {      // ill-formed
void F() {  // OK: definition of F
}- end example
```

An identifier can optionally be paired as a parameter name: [Note: In particular, parameter names are also optional in function definitions (11.4), it names a parameter used for a parameter in different declarations and the definition of a function must not be the same. If a parameter name present in a function declaration that is not a definition, it cannot be used outside of its function declarator because the extent of its potential scope (6.4) — end note]

Example: The declaration

```
int : *pi,
f(),
*pi(int),
(*fpi(const char*, const char*),
(*fpip(int));
```

declares an int, a pointer pi to int, a function f taking no arguments and returning an integer, a function fpi taking an integer argument and returning a pointer to int, a pointer fpip taking two pointers to constant characters and returning an integer, returning a pointer to a function that takes an integer argument and returns an integer. It is especially useful to compare f and fpi. The binding of *pi(int) is *f*(fpi(int)) — [Note: Typedefs and trailing-return-types are sometimes convenient when the return type of a function is complex. For example, the function fpip could have been declared without the parentheses (which would yield an int (*)() to indicate that a pointer to a function yields a char*), the declarator — end example]

```
typedef int IFUNC(int);
FPPI(int);
```

or

```
auto fpip(int)->int(*);
A trailing-return-type is most useful for a type that would be more complicated to specify before the declarator-id:
```

```
template <class T, class U> auto add(T t, U u) -> decltype(t + u);
rather than
```

```
template <class T, class U> decltype((*T)(0) + (*U)(0)) add(T t, U u);
— end note
```

A non-function is a function that is not a template specialization. [Note: A function template is not a function. — end note]

A declarator-id or abstract-declarator containing an ellipsis shall only be used in a parameter-declaration. Such a parameter-declaration pack (17.5.3). When it is part of a parameter-declarator-clause, the parameter pack is a function pack (17.5.3). [Note: Otherwise, the parameter-declaration is part of a template-parameter-list and the parameter pack is a template pack; see 17.1. — end note] A function pack is a pack expansion (17.5.3). [Example:

```
template<typename T> void f(T (...t)(int, int));

int add(int, int);
float subtract(int, int);

void g() {
    f(add, subtract);
}
```

— example
There is a syntactic ambiguity when an ellipsis occurs at the end of a parameter-declaration-clause without a preceding comma. In this case, the ellipsis is parsed as part of the abstract-declarator if the parameter either names a template pack that has not been expanded or contains auto; otherwise, it is parsed as part of the parameter-declaration-clause.

## 11.3.6 Default arguments [dcl.ft.default]

If an initializer-clause is specified in a parameter-declaration this initializer-clause is used as a default argument. Default arguments will be used in cases where trailing arguments are missing.

[Example: The declaration
void point(int = 3, int = 4);
declares a function that can be called with zero, one, or two arguments of type int. It can be called in part of these ways:
point(1,2); point(1);
The last two are equivalent to point(1,4) and point(3,4). — end example

A default argument should be specified only in the parameter-declaration-clause of a function declaration or lambda-expression. In the latter case, the initializer-clause shall be an assignment. A default argument shall not be specified for a parameter pack. If it is specified in a parameter-declaration-clause, it shall not occur within a declarator or abstract-declarator of a function.

For template functions, default arguments can be added in later declarations of a function in the same scope. Declarations in different scopes have completely distinct sets of default arguments. That is, declarations in inner scopes do not acquire default arguments from outer scopes, and vice versa. In a given declaration, each parameter subsequent to a function with a default argument must have a default supplied in this or previous declaration. A default argument shall not be redefined by a later declaration (not even to same value). [Example:

```
void g(int = 0, ...); // OK, ellipsis is not a parameter so it can follow
void point(int, int); // parameter with default argument
void f(int = 5);
```

+ 101 One can explicitly disambiguate the parse by introducing a comma (so the ellipsis will be parsed as part of the parameter-declaration-clause) or by introducing a name for the parameter (so the ellipsis will be parsed as part of the declaration).

+ 102 This means that default arguments cannot appear, for example, in declarations of pointers to functions, references to functions, or typedef declarations.

```
void f(int = 1, int); // error: does not use default from surrounding scope
void m() {
    void f(int, int); // has no defaults
    void f(int, = 5); // error: wrong number of arguments
    f(4); // OK
    f(4, 5); // OK
    void f(int, = 5); // error: cannot redefine to same value
}
void n() {
    f(6); // OK, calls f(6)
}
```

- For given inline function defined in different translation units, the sets of default arguments in a declaration of the translation units will be the same; If a friend-relation specifies a default argument expression, that declaration shall be a definition and the only declaration of the function or template in the translation unit. The default argument has the same constraints as the initializer of a variable of the same type, using copy-initialization semantics [6.6]. The names in the default argument are bound, and the semantic constraints are checked at the point where the default argument is used. Lookup and checking of semantic constraints for default arguments in function templates and member functions of class templates are performed as described in [6.4.1]. In the following code, g will be called with the value f(2);

```
int a;
int f(int);
int g = f(a); // default argument: ::a
void h() {
    int a = 2;
    int a = 3;
    g(); // f(::a)
}
```

- [Note: In member function declarations, names in default arguments are looked up as described in Clause 14. — end note]; Except for member functions of class templates, the default arguments in a member function that appears outside of the class definition are provided by the function declaration in the class definition; the program is ill-formed if a default constructor [15.1], copy or move constructor, copy or move assignment operator [15.8] is declared. Default arguments for a member function of a class template shall be specified on the initial declaration of the member function within the class template. [Example]:

```
class C {
    void f(int i = 3);
    void g(int i, int j = 9);
}
```

```
void C::f(int) {} // error: default argument already specified in class scope
void C::g(int i = 88, int j) {} // in this translation unit, C::g can be called with no argument
```

- example example

7 A local variable shall not appear as a potentially-evaluated expression in a default argument. [Example:

```
void f() {
    int i;
    extern void g(int x = i); // error
    extern void h(int x = sizeof(i)); // OK
    // ...
}
```

[Note: The keyword may not appear in a default argument of a member function; see 8.1.2. [Example:

```
class A {
    void f(A* p = this) {
}; // error
```
[ end example] -- end

9 A default argument is evaluated each time the function is called with no argument for the corresponding parameter. A parameter shall not appear as a potentially-evaluated expression in a default argument. Parameters of a function declared before a default argument are in scope and can hide namespace and class member names. [Example:

```
int a;
int f(int a, int b = a); // error: parameter a used as default argument
typedef int;
int g(float I, int b = I(2)); // error: parameter I found
int h(int a, i = b); // OK: use unused operand
```
[ end example] A non-static member shall not appear in a default argument unless it appears the id-expression of class member access (8.2.5) unless it is used to form a pointer to member (8.3.1). [Example: The declaration of X::mem1() in the following example is ill-formed because no object is needed for the non-static member X::mem1() as an initializer.

```
int b;
class X {
    int a;
    int mem1(int i = a); // error: non-static member used as default argument
    int mem2(int i = b);
    static int b;
}
```

The declaration of X::mem2() is meaningful, however, since no object is needed to access the static member X::. Classes, objects, and members are described in Clause 12. [end example]

- A default argument is not part of the type of a function(0). [Example:

```
int f(int)
void h() {
    int j = f(1);
    int k = f(0);
}
```

```
int (*p1)(int) = &f;
int (*p2)(int) = &f; // error: type mismatch
```

[ end example]
