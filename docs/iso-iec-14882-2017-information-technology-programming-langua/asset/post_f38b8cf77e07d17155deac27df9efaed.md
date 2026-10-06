
# ISO/IEC 14882:2017(E)

2 A template argument list may be specified when referring to a specialization of a function template

- (2.1) when a function is called,
- (2.2) when the address of a function is taken, when a function initializes a reference to function, or when a pointer to member function is formed,
- (2.3) in an explicit specialization,
- (2.4) in an explicit instantiation, or
- (2.5) in a friend deduction.

3 Trailing arguments that can be deduced (17.8.2) or obtained from default template-arguments may not otherwise deduced from the list of explicit template-arguments. A trailing parameter pack (17.5.3) may be deduced to an empty sequence of template arguments. If all of the template arguments can be deduced, they may be omitted; in this case, the template argument list <> may be omitted. In contexts where deduction is done and fails, or in contexts where deduction identifies a single function specialization, then the template-id is an invalid for the function specialization. [Example:

```
template<class X, class Y> X(Y, class ... -> Z) g(Z);
int i = f(5);      // Y is deduced to be double
int j = f(6);       // ill-formed: X cannot be deduced
void f0(int f);     // Y for outer f deduced to be int (*) (bool)
void f1(int f);     // ill-formed: f0 cannot deduce a single function template specialization
int k = g(5);       // Y is deduced to be double, Z is deduced to an empty sequence
void f2(int f);     // Y for outer f is deduced to be int (*) (bool)
```

— end example

4 An empty argument list can be used to indicate that a given use refers to a specialization of a function event when a non-template function (11.3.5) is visible that would otherwise be used. For example:

```
template<class T> int f(T);  // #1
int f(int);             // #2
int k = f(1);           // uses #2
int l = f<int>(1);      // uses #1
```

5 Template arguments that will be presented in the declaration order of their corresponding template-parameters. The template argument list shall not specify more template-arguments than there are corresponding template-parameters unless one of the template is a template parameter pack. [Example:

```
template<class X, class Y, class Z> X f(Y,Z);
template<class... Args> void f2(Args);
void g() {
  f(const, char*, double)("aa",3.0); // Y is deduced to be double
  f(int, const char*)("aa",3.0);    // Y is deduced to be const char*, and Z is deduced to double
  f("aa",3.0);                      // error: X cannot be deduced
  f(char, short, int, long);       // OK
```

— end example

6 Implicit conversions (Clause 7) will be performed on a function argument to convert it to the type of the corresponding function parameter if the parameter type contains template-parameters that participate in template argument deduction. [ Note: Template parameters do not participate in template argument deduction if they are explicitly specified. For example,

```
template<class T> void f(T);

class Complex {
 Complex(double);
};

void g() {
 fComplex(i); // OK, means fComplex<Complex>(i)
}
```

— end note

7 [ Note: Because the explicit argument list lists the function template name, and base conversion member functions and constructor member functions called without using a function name, there is no way to provide an explicit template argument list for these templates. — end note|

8 [ Note: For simple function names, argument lookup (6.4.2) applies even when the function name is not visible within the scope of the call. But when a function with explicit template arguments is used, the call will have the syntactic form of a call (6.4.1), which does not have the correct syntactic form unless there is a function with that name at the point of the call. If no such name is visible, it is syntactically well-formed and argument-dependent lookup does not apply to such name; argument-dependent lookup applies and additional function templates may be found in other namespaces. Example|

```
namespace A {
 struct B {
 template<typename X> void f(B);
}

namespace C {
 template<class T> void f(T);
}

void g(A::B a; B b) {
 f<B>(b); // ill-formed: not a function call
 A::f(b); // well-formed
 C::f(b); // ill-formed; argument-dependent lookup applies only to unqualified names
 using: C;
 f<B>(b); // well-formed because C::f is visible; A::f is found by argument dependent lookup
}
```

— end example

9 Template argument deduction can extend the sequence of template arguments corresponding to a template parameter pack, even when the sequence explicitly specified template arguments. Example|

```
template<class Types> void f(Types);
```
