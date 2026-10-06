# ISO/IEC 14882:2017(E)

(2.1) If A is an array type, the type produced by the array-to-pointer standard conversion (7.2) is used in place of A for type deduction; otherwise;

(2.2) If A is a function type, the type produced by the function-to-pointer standard conversion (7.3) is used in place of A for type deduction; otherwise;

(2.3) If A is a cv-qualified type, the top-level cv-qualifiers of A are ignored for type deduction.

3 If P is a cv-qualified type, the top-level cv-qualifiers of P’s type are ignored for type deduction. If P is a reference type, the type referred to by P is used for type deduction. [Example]:

```
template <class T> int f(const T)
int n1 = f(0); // calls f<int>(const int)
int i = 0;
int n2 = f(i); // calls f<int>(const int)
template <class T> int g(volatile T)
int n3 = g(i); // calls g<int>(volatile int)
```

// example: A forward reference to a cv-unqualified pointer parameter that does not represent a parameter of a class template (class argument reference (16.3.1.8)). If P is a reference type and the argument is a, the type "value reference to A" is used in place of A for type deduction. [Example]:

```
template <class T> int f(T& reference);
template <class T> int g(const T&);
int i = 0;
int n1 = f(i); // calls f<int>(int&)
int n2 = f(0); // calls f<int>(const int&)
int n3 = g(i); // error: would call g<int>(const int), which would bind an reference to an lvalue
```

```
template <class T> struct A {
template <class U>
A(T& U, int*); // #1: T& is not a forward reference.
U& is a forward reference.
A(T&, int*); // #2
};
```

```
template <class T> A(T&, int*); // #3: T& is a forward reference.
```

```
int* ip;
A(1, ip); // error: cannot deduce from #1
A(a0, ip); // uses #1 to deduce A<int> and #1 to initialize
A(a2, ip); // uses #3 to deduce A<int> and #2 to initialize
// example
```

4 In general, the deduction process attempts to find argument values that make the deduced A identical to A (after the type is transformed). However, there are three cases that allow a difference:

+   - If the original P is a reference type, the deduced A (i.e., the type referred to by reference) can be more cv-qualified than the transformed A

+   - The transformed A can be another pointer or member type that can be converted to the deduced A via a pointer conversion (7.13) and/or quality conversion (7.5)

+   - If P is a class and has the simple-template-id, the transformed A can be a derived class of the deduced A. Likewise, if P is a pointer to a class of the simple-template-id, the transformed A can be a pointer to a derived class to the deduced A.