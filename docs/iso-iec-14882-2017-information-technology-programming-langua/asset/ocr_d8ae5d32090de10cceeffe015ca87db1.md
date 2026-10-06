# ISO/IEC 14882:2017(E)

the member template name shall be prefixed by the keyword template. [Example: 

```
struct X {
    template<size_t> X alloc();
    template<size_t> static X adjust();
};

template<class T> void f(T* p) {
    T* q = p->alloc<200>();
    T* r = p->alloc<200>();
    T::adjust(100);
    T::adjust(100);
}
```

// end example
A name prefixed by the keyword template shall be a template-id or the name shall refer to a class template or an alias template. [Note: The keyword template may not be applied to non-template members of class templates. - end note] [Note: As is the case with the typename prefix, the prefix is allowed in cases where it is not strictly necessary; i.e., when the nested-name-specifier, or the expression on the left of the -> is not dependent on a template-parameter, or use does not appear in the scope of a template. - end note] Example: 

```
template<class T> struct A {
    void f();
    template<class U> void u();
};

template<class T> void f(T* t) {
    A<T> a(t);
    a.template f(t);
    a.template f(t);
}

template<class T> struct B {
    template<class T2> struct C {};
}
```

// ill-formed: < less than
// OK: < starts argument list
// ill-formed: < less than
// OK: calls template
// error: not a template-id

// OK: T::template C names a class template:
template<class T, template <class I> class TT = T::template <O> struct D {};
<B<int>> db;

// end example

+   6. A simple-template-id that names a class specialization is a class-name (Clause 12).
7. A template-id that names an alias template specialization is a type-name.

# 17.3 Template arguments [temp.arg]

There are three forms of template-argument, corresponding to the three forms of template-parameter: type, non-type and template. The type and form of each template-argument specified in a template-id shall match the type and form specified for the corresponding parameter declared by the template in its template-parameter-list. When the parameter declared by the template is a template pack (17.5.3), it will correspond to zero or more template-arguments. Example: 

```
template<class T> class Array {
    T* v;
    int sz;
public:
```