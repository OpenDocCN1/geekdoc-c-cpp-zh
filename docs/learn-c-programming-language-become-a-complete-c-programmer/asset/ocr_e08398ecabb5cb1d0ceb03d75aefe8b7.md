function memcpy() when we can treat the objects as “plain old data” (POD; §8.2.6). If not, we copy the objects one by one (potentially) using their copy constructor. We determine whether the template argument type is a POD by the standard-library type predicate is_pod. The result is presented by the member value. This standard-library convention is similar to the way type functions present their result as a member type.

The std::is_pod predicate is one of the many provided by the standard library (§35.4.1). Since the rules for being a POD are tricky, is_pod is most likely a compiler intrinsic rather than implemented in the library as C++ code.

Like the ::type convention, the value ::value causes verbosity and is a departure from conventional notation that lets implementation details shine through: a function returning a bool should be called using ():

```
template<typename T>
void copy(T* p, const T* q, int n)
{
if (is_pod<T>())
// ...
}
```

Fortunately, the standard supports that for all standard-library type predicates. Unfortunately, for language-technical reasons, this resolution is not available in the context of a template argument. For example:

```
template<typename T>
void do_something()
{
Conditional<is_pod<T>(),On_heap<T>,Scoped<Y>> x; // error :is_pod<T>() is a type
// ..
}
```

In particular, is_pod<T> is interpreted as the type of a function taking no argument and returning an is_pod<T> (§iso.14.3[2]).

My solution is to add functions to provide the conventional notation in all contexts:

```
template<typename T>
constexpr bool Is_pod()
{
return std::is_pod<T>::value; }
```

# Section 28.2.2 Type Predicates 787

I capitalize the names of these type functions to avoid confusion with the standard-library versions. In addition, I keep them in a separate namespace (Estd).

We can define our own type predicates. For example:

```
template<typename T>
constexpr bool Is_big()
```