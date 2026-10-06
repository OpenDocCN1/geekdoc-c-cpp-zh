# ISO/IEC 14882:2017(E)

```
(8.1) — no valid specialization can be generated for a template or a substatement of a constexpr pr if state-
(9.4.1) within a template and the template is not instantiated, or
```

```
(8.2) — every specialization of a variadic template requires an empty template parameter pack, or
```

```
(8.3) — a hypothetical instantiation of a template immediately following its definition will be ill-formed due
to a construct that does not depend on a template parameter, or
```

```
(8.4) — the interpretation of such a construct in the hypothetical instantiation is different from the interpretation
of the corresponding construct in any actual instantiation of the template. [Note: This can happen in-
stantiating the following:
```

```
(8.4.1) — a used in a non-dependent name is incomplete at the point at which a template is defined
but is complete at the point at which an instantiation is performed, or
```

```
(8.4.2) — lookup for a name in the template definition finds a using-declaration,
corresponding scope in the instantiation does not find any declarations because the using-declaration
was a expansion and the corresponding pack is empty, or
```

```
(8.4.3) — an instantiation uses a default argument or default template argument that had not been
def at the point at which the template was defined, or
```

```
(8.4) — constant expression instantiation (8.20) within the template instantiation uses
```

```
(8.4.1) — the value of a const object of integral or unescaped enumeration type or
```

```
(8.4.2) — the value of a constexpr object
```

```
(8.4.3) — the value of a reference or
```

```
(8.4.4) — the definition of a constexpr function,
and that was not defined when the template was defined, or
```

```
(8.4.5) — a class template specialization or variable specialization that is specified by a non-
dependent simple-template-id is used by the template, and either it is instantiated from a partial
specialization that was not defined when the template was defined or it names an explicit
specialization that was not declared when the template was.
```

```
— end note]
```

Otherwise, no diagnostic should be issued for a template for which a valid specialization can be generated.
[Note: If a template is instantiated, errors will be diagnosed according to the other rules in this document.
— end note] Example:
Exactly when these errors are diagnosed is a quality of implementation issue.

```
int;
template<class T> class X {
void f(T t, int i, char p) {
	t = i;           // may be diagnosed if X::f is instantiated, and the assignment to t is an error
	p = 1;           // may be diagnosed if X::i is not instantiated
	p = j;           // may be diagnosed if X::f is not instantiated
}

void g(T t) {
	*;\             // may be diagnosed if X::g is not instantiated
}

template<class... T> struct A {
void operator++(int, T...) {
	} // error: too many parameters
}
tntemplate<class... T> union A : T... { };
                               // error: union with base class
template<class... T> struct A : T... { T... { };
                               // error: duplicate base class
```

§ 17.6

©ISO/IEC 2017 — All rights reserved

375