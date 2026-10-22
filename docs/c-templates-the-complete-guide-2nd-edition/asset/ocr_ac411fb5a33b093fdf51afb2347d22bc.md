In most contexts, multiple type trait predicates can be combined by using logical operators. However, in some contexts of template metaprogramming, this is not enough: • If you have to deal with traits that might fail (e.g., due to incomplete types). • If you want to combine type trait definitions.

The type traits std::conjunction<>, std::disjunction<>, and std::negation<> are provided for this purpose.

One example is that these helpers short-circuit Boolean evaluations (abort the evaluation after the first false for && or first true for ||, respectively).¹⁴ For example, if incomplete types are used: Click here to view code image

```
struct X {
X(int); // converts from int
};
struct Y; // incomplete type
```

the following code might not compile because is_constructible results in undefined behavior for incomplete types (some compilers accept this code, though): Click here to view code image

```
// undefined behavior:
static_assert(std::is_constructible<X, int>{} || std::is_constructible<Y, int>{}, "can't init X or Y from int");
```

Instead, the following is guaranteed to compile, since the evaluation of is_constructible<X,int> already yields true: Click here to view code image

```
// OK:
static_assert(std::disjunction<std::is_constructible<X, int>, std::is_constructible<Y, int>>{}, "can't init X or Y from int");
```

The other application is an easy way to define new type traits by logically combining existing type traits. For example, you can easily define a trait that checks whether a type is “not a pointer” (neither a pointer, nor a member pointer, nor a null pointer): Click here to view code image

```
template<typename T>
struct isNoPtrT :
std::negation<std::disjunction<std::is_null_pointer<T>,
std::is_member_pointer<T>,
std::is_pointer<T>>>
{};
```

Here we can’t use the logical operators, because we combine the corresponding trait classes. With this definition, the following is possible: Click here to view code image

```
std::cout << isNoPtrT<void*>::value << '\n'; //false
```