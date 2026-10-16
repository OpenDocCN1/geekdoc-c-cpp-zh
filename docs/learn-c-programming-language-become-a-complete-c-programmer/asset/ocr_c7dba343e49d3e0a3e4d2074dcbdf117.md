```
return g(a); // OK: a is a dependent name and therefore so is g }
class Quad { /*...*/ }; void g(Quad);
int z = f(Quad{2}); // f’s gisbound to g(Quad)
```

A call that by coincidence has an argument that matches an actual template parameter type is not dependent. For example:

```
class Quad { /*...*/ };

template<typename T> T ff(T a)
{
return gg(Quad{1}); // error :no gg() in scope and gg(Quad{1}) doesn’t depend on T }
int gg(Quad);

int zz = ff(Quad{2});
```

Had gg(Quad{1}) been considered dependent, its meaning would have been most mysterious to a reader of the template definition. If a programmer wants gg(Quad) to be called, gg(Quad)’s declaration should be placed before the definition of ff() so that gg(Quad) is in scope when ff() is analyzed. This is exactly the same rule as for non-template function definitions (§26.3.2).

By default, a dependent name is assumed to name something that is not a type. So, to use a dependent name as a type, you have to say so, using the keyword typename. For example:

```
template<typename Container>
void fct(Container& c)
{
Container::value_type v1 = c[7]; // syntax error:value_type is assumed to be a non-type name typename Container::value_type v2 = c[9]; // OK: value_type assumed to name a type auto v3 = c[11]; // OK: let the compiler figure it out // ...
```

We can avoid such awkward use of typename by introducing a type alias (§23.6). For example:

```
template<typename T>
using Value_type<T> = typename T::value_type;

template<typename Container> void fct2(Container& c)
{
Value_type<Container> v1 = c[7]; // OK
// ...
}
```

Naming a member template after a . (dot), ->, or :: requires similar use of the keyword template. For example:

```
class Pool { // some allocator
public:
template<typename T> T* get();
template<typename T> void release(T*);
// ...
```