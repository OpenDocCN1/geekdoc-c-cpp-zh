# ISO/IEC 14882:2017(E)

- end example[]

[Note: A string literal (5.13.5) is not an acceptable template-argument. [Example:
template<class T, const char*> class X {
/* ... */
};
xint, "Studebaker" x1; // error: string literal as template-argument
const char[p] = "Vivectionist";
xint,p> x2; // OK
- end example | - end note]

[Note: The address of an element or non-static data member is not an acceptable template-argument. [Example:
template<int> p class X { };
int[10(
struct S { int m; static int s; };
x[a]> x3; // error: address of array element
x&s.m> x4; // error: address of non-static member
x&s x5; // OK: address of static member
x&s x6; // OK: address of static member
- end example | - end note]

Note: A temporary object is not an acceptable template-argument when the corresponding template-argument has reference type. [Example:
template<const int&> struct B { /* ... */ };
B c1;
int c = 1;
c< b1; // error: temporary would be required for template argument
- end example | - end note]

# 17.3.3 Template template arguments

A template-argument for a template-parameter should be the name of a class template or an alias template, expressed as id-expression. When the template-argument names a class template, only primary class templates are considered when matching the template argument with the corresponding parameter; partial specializations are not considered if their parameter lists match that of the template parameter.

Any partial specializations associated with the primary class template or primary variable are considered when a specialization based on the template-parameter is instantiated. If a specialization is not visible at the point of instantiation, and it would have been selected had it visible, a diagnostic is required. [Example:
template<class T> class A {
int x;
};
template<class T> class A<T*> { // partial specialization
long x;
};

§ 17.3.3 ISO/IEC 2017 - All rights reserved 352