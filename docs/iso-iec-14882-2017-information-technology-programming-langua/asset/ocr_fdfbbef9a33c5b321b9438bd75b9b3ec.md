# ISO/IEC 14882:2017(E)

(3.2.2) the rank of S1 is better than the rank of S2, or S1 and S2 have the same rank and are distinguishable by the rules in the paragraph below, or if not that,

(3.2.3) S1 and S2 are reference bindings (11.63) and neither refers to an implicit object parameter of a non-static member function declared without a ref-qualifier, and S1 binds an rvalue reference to an rvalue and S2 binds an rvalue reference [Example:

```
int i;
int f1();
int& f2();
int g(const int&);
int g(const int&);
int j = g(i); // calls g(i)
int k = g(f1()); // calls g(const int&)
int l = g(f2()); // calls g(const int&)

struct A {
A& operator<<(int);
void p();
void p(int&);
};
A& operator<<=(const A&, char,);
A << 1; // calls A::operator<<(int)
A << 'c'; // calls A::operator<<(A&, char)
A;
na << 1; // calls A::operator<<(int)
A << 'c'; // calls A::operator<<(int)
a.p(); // calls A:p(p)
a.p(); // calls A:p(p)
```

(3.2.4) end example]; or if not that,
s1 and S2 are reference bindings (11.63) and S1 binds an rvalue reference to a function value [Example:

```
int f(void())); // #1
int f(void(&)); // #2
void g();
int ii = f(g()); // or if not that,
```

(3.2.5) S1 and S2 differ only in their qualification conversion and yield similar types T1 and T2 (7.5), respectively, and the cv-qualification signature of type T1 is a proper subset of the cv-qualification signature of type T2 [Example:

```
int f(const volatile int*);
int f(const int*);
int i;
j = f(&i); // calls f(const int*)
 example]; or, if not that,
```

(3.2.6) S1 and S2 are reference bindings (11.63), and the types to which the reference refers are the same type except for top-level cv-qualifiers, and the type to which the reference initialized by S2 is more cv-qualified than the type to which the reference initialized by S1 refers. [Example:

```
int f(const int&);
int f(const int&);
 g(const int&);
```

§ 16.3.3.2

©ISO/IEC 2017 - All rights reserved

331