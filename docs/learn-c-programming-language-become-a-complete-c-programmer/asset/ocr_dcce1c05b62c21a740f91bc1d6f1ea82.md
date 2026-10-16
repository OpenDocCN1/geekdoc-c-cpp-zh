```
};
void Derived::f() final // error :final out of class {
// ...
}
```

Section 20.3.4.2 final 593

```
void g() final // OK {
// ...
}
```

Like override (§20.3.4.1), final is a contextual keyword. That is, final has a special meaning in a few contexts but can be used as an ordinary identifier elsewhere. For example:

```
int final = 7;
struct Dx : Base { int final;
int f() final
{
return final + ::final;
}
};
```

Don’t indulge in such cleverness; it complicates maintenance. The only reason that final is a contextual keyword, rather than an ordinary keyword, is that there exist a significant amount of code that has used final as an ordinary identifier for decades. The other contextual keyword is override (§20.3.4.1).

# 20.3.5 using Base Members

Functions do not overload across scopes (§12.3.3). For example:

```
struct Base {
void f(int);
};
```

```
struct Derived : Base { void f(double);
};
```

```
void use(Derived d) {
d.f(1); // call Derived::f(double)
Base& br = d
br.f(1); // call Base::f(int)
}
```

This can surprise people, and sometimes we want overloading to ensure that the best matching member function is used. As for namespaces, using-declarations can be used to add a function to a scope. For example:

```
struct D2 : Base {
using Base::f; // bringall fs from Base into D2
void f(double);
```