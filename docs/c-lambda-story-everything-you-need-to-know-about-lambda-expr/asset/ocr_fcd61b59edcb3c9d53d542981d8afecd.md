Because myLambda is just a stateless lambda, it’s also an empty class, without any data member fields, so its minimal size is only one byte. On the other hand, the std::function version is much larger - 32 bytes. That’s why you can, rely on the auto type deduction to get the smallest possible closure objects.

When we talk about std::function , it’s also important to mention that this type doesn’t support movable-only closures. You can read more about this issue in the C++14 chapter on movable types.

# Constructors and Copying

In the specification of the feature at [expr.prim.lambda] we can also read the following:

| The closure type associated with a lambda-expression has a deleted (ldcl.fct.def.delete) default constructor and a deleted copy assignment operator. |

That’s why you cannot write:

```
auto foo = [&x, &y]() { ++x; ++y; };
decltype(foo) fooCopy;
```

This gives the following error on GCC:

```
error: use of deleted function 'main()::<lambda<>()()'
decltype(foo) fooCopy;
~~~
```

note: a lambda closure type has a deleted default constructor

However, you can copy lambdas:

Copying lambdas. Live code @Wbox

```
#include <type_traits>
int main () {
    const auto firstLam = [](int x) noexcept { return x * 2; };
    const auto secondLam = firstLam;
    static_assert(std::is_same<firstLam, decltype(secondLam)>::
value,
    "must be the same";
}
```