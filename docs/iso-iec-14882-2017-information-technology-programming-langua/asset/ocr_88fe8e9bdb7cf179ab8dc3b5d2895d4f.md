# ISO/IEC 14882:2017(E)

7 A local variable shall not appear as a potentially-evaluated expression in a default argument. [Example:

```
void f() {
    int i;
    extern void g(int x = i);    // error
    extern void h(int x = sizeof(i)); // OK
    // ...
}
```

 [Note: The keyword may not appear in a default argument of a member function; see 8.1.2. [Example:

```
class A {
    void f(A* p = this) {
    };
 // error
```

[ end example] -- end
9 A default argument is evaluated each time the function is called with no argument for the corresponding parameter. A parameter shall not appear as a potentially-evaluated expression in a default argument. Parameters of a function declared before a default argument are in scope and can hide namespace and class member names. [Example:

```
int a;
int f(int a, int b = a);      // error: parameter a used as default argument
typedef int;
int g(float I, int b = I(2));  // error: parameter I found
int h(int a, int i = b);      // OK: use unused operand
```

[ end example] A non-static member shall not appear in a default argument unless it appears the id-expression of a class member access (8.2.5) unless it is used to form a pointer to member (8.3.1). [Example: The declaration of X::mem1() in the following example is ill-formed because no object is needed for the non-static member X::mem1() as an initializer.

```
int b;
class X {
    int a;
    int mem1(int i = a);      // error: non-static member used as default argument
    int mem2(int i = b);
    static int b;
}
```

The declaration of X::mem2() is meaningful, however, since no object is needed to access the static member X::. Classes, objects, and members are described in Clause 12. [end example] A default argument is not part of the type of a function(0). [Example:

```
int f(int)
nvoid h() {
    int j = f(1);
    int k = f(0);
}
```

```
int (*p1)(int) = &f;
int (*p2)(int) = &f;      // error: type mismatch
```

[ end example] When a declaration of a function is introduced by way of a using-declaration(10.3.3), any default argument information associated with the declaration is known as well. If the function is redeclared thereafter in the namespace with additional default arguments, the additional arguments are also known at any point following the redeclaration where the using-declaration is in scope.

§ 11.3.6 ©ISO/IEC 2017 - All rights reserved 215