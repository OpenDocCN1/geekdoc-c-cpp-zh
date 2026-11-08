```
```cpp
#include "Lesson.hpp"

template<typename T>
struct IsDefaultConstructible {
 private:
   // test() trying substitute call of a default constructor
   template<typename U, typename = decltype(U())>
   static char test(void*);

   // test() fallback
   template<typename>
   static long test(...);

 public:
   static constexpr bool value
     = sizeof(test<T>(nullptr)) == sizeof(char);
};
```
```

The usual approach to implement a SFINAE-base trait with function overloading is to declare two overloaded function templates named `test()` with different return types:

Click here to view code image

```
```cpp
template<class T> static char test(T*);
template<class> static long test(...);
```
```

The first overload is designed to match only if the requested check succeeds (we will discuss below how that is achieved). The second overload is the fallback. It always matches the call, but because it matches "with ellipses," a variadic parameter), any other match would be preferred (see Section C.2 on page 86).

Our return value “value” depends on which overloaded `test()` member is selected:

Click here to view code image

```
```cpp
static constexpr bool value
  = IsSame<decltype(test<T>(nullptr)), char>::value;
```
```

If the first `test()` member—when return type is `char`—is selected, `value` will be initialized to `true` thanks to `sizeof(char) == sizeof(char)`. Otherwise, it will be initialized to `false` because `sizeof(long) != sizeof(char)`.

Now, we have to deal with the specific properties we want to test. The goal is to make the first `test()` overload valid if and only if the condition we want to check applies. In this case, we want to find out whether we can default construct an object of the passed type `T`. To achieve this, we pass `T` and a `void` sign of first declaration of `test()` around (namely, template argument initialization with an abstract that is valid if and only if the conversion is valid). In this case, we use the expression that can only be valid if an implicit or explicit default constructor exists: `U()`. The expression is surrounded by `decltype` to make this a valid expression to initialize a type parameter.

The second template parameter cannot be deduced, so no corresponding argument is passed. And we will not provide an explicit template argument for it. Therefore, it will be substituted, and if the substitution fails, according to SFINAE, that declaration of `test()` will be discarded so that only the fallback function will match.

Thus, we can use the trait as follows:

Click here to view code image

```
```cpp
IsDefaultConstructible<int>::value  //yields true

struct S {
  S() = delete;
};

IsDefaultConstructible<S>::value    //yields false
```
```

Note that we can use the template parameter `T` in the first `test()` directly: