```
class X : public T {
public:
typename T::Type m; // OK
Type m2; // error (no Type in scope)
using T::g2(); // bring T::g2() into scope

void f() {
this->g(2); // call T::g
g(2); // call ::g(int); surprise? g2(2); // call T::g2
}
// ...
};

void h(X<B> x)
{
x.f();
}
```

Only at the point of instantiation can we know if the argument used for the parameter T (here B) has the required names.

It is easy to forget to qualify names from a base, and the qualified code often looks a bit verbose and messy. However, the alternative would be that a name in a template class would sometimes bind to a base class member and sometimes to a global entity depending on the template argument. That is not ideal either, and the language rule supports the rule of thumb that a template definition should be as self-contained as possible (§26.3).

Qualifying access to dependent base members of a template can be a nuisance. However, explicit qualifications help maintainers, so the initial author shouldn’t grumble too much about the extra typing. A common occurrence of this problem is when a whole class hierarchy is templatized. For example:

```
template<typename T>
class Matrix_base { // memory for matrices,operations of all elements
// ...
int size() const { return sz; }
protected:
int sz; // number of elements
T* elem; // matrixelements
};
```

```
template<typename T, int N>
class Matrix : public Matrix_base<T> { // N-dimensional matrix // ...
T* data() // return pointer to element storage
{
return this->elem;
}
};
```

Here, the this-> qualification is required.