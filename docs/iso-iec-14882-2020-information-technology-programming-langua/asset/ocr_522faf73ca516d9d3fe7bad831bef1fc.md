```
g();
}
}
```

```
// g(f(::a))
```

— end example

> [Note 3: In member function declarations, names in default arguments are looked up as described in 6.5.2. Access checking applies to names in default arguments as described in 11.9. — end note]

6 Except for member functions of class templates, the default arguments in a member function definition that appears outside of the class definition are added to the set of default arguments provided by the member function declaration in the class definition; the program is ill-formed if a default constructor (11.4.5.2), copy or move constructor (11.4.5.3), or copy or move assignment operator (11.4.6) is so declared. Default arguments for a member function of a class template shall be specified on the initial declaration of the member function within the class template.

[Example 4:

```
class C {
    void f(int i = 3);
    void g(int i, int j = 99);
};
```

```
void C::f(int i = 3) {}        // error: default argument already specified in class scope
void C::g(int i = 88, int j) {} // in this translation unit, C::g can be called with no argument
```

— end example

> 7 [Note 4: A local variable cannot be odr-used (6.3) in a default argument. — end note]

[Example 5:

```
void f() {
    int i;
    extern void g(int x = i);        // error
    extern void h(int x = sizeof(i)); // OK
    // ...
}
```

— end example

> 8 [Note 5: The keyword this cannot appear in a default argument of a member function; see 7.5.2.

[Example 6:

```
class A {
    void f(A* p = this) { }        // error
};
```

— end example

— end note

9 A default argument is evaluated each time the function is called with no argument for the corresponding parameter. A parameter shall not appear as a potentially-evaluated expression in a default argument. Parameters of a function declared before a default argument are in scope and can hide namespace and class member names.

[Example 7:

```
int a;
int f(int a, int b = a);            // error: parameter a used as default argument
typedef int I;
int g(float I, int b = I(2));        // error: parameter I found
int h(int a, int b = sizeof(a));      // OK, unevaluated operand
```

— end example

A non-static member shall not appear in a default argument unless it appears as the id-expression of a class member access expression (7.6.1.5) or unless it is used to form a pointer to member (7.6.2.2).

[Example 8: The declaration of X::mem1() in the following example is ill-formed because no object is supplied for the non-static member X::a used as an initializer.

```
int b;
```