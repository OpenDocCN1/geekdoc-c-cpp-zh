| Trait | Effect |
|---|---|
| `is_nothrow_destructible<T>` | Can trivially destroy a `T` and that operation can't throw. |
| `is_swappable<T>` | Can call `swap(t, u)` for this type (since C++17). |
| `is_nothrow_swappable<T>` | Can call `swap(t, u)` for this type and that operation can't throw (since C++17). |
| `is_swappable_with<T, U>` | Can call `swap(t, u)` for these two types with specific value category (since C++17). |
| `is_nothrow_swappable_with<T, U>` | Can call `swap(t, u)` for these two types with specific value category and that operation can't throw (since C++17). |

*Table 8.4. Traits to Check for Specific Operations*

Table 8.4 lists the type traits that allow us to check for some specific operations. The forms with `is_trivially_...` additionally check whether all (sub-)operations called for the object members or base classes are trivially (neither user-defined nor virtual). The forms with `is_nothrow_` additionally check whether the called operation guarantees not to throw. Note that all `is_..._constructible` checks imply the corresponding `is_..._destructible` check. For example:

**Click here to view code image**

`util/isconstructible.cpp`

```
```cpp
#include <iostream>

class C {
 public:
  C() { // default constructor has no noexcept
  }
  virtual ~C() = default; // makes C nontrivial
};

int main()
{
  using namespace std;
  cout << is_default_constructible_v<C> << '\n';
  cout << is_trivially_default_constructible_v<C> << '\n';
  cout << is_nothrow_default_constructible_v<C> << '\n';
  cout << is_copy_constructible_v<C> << '\n';
  cout << is_trivially_copy_constructible_v<C> << '\n';
  cout << is_nothrow_copy_constructible_v<C> << '\n';
  cout << is_destructible_v<C> << '\n';
  cout << is_nothrow_destructible_v<C> << '\n';
}
```
```

Due to the definition of a virtual destructor, all operations are no longer trivial. And because we define a default constructor without `noexcept`, it might throw. All other operations, by default, guarantee not to throw.

+   - `std::is_constructible<T, Args...>::value`
+   - `std::is_trivially_constructible<T, Args...>::value`
+   - `std::is_nothrow_constructible<T, Args...>::value`

Yields true if an object of type `T` can be initialized with arguments of the types given by `Args...` (without using a nontrivial operation or with the guarantee that no exception is thrown). That is, the following must be valid:

`T t(std::declval<Args>()...);`

A true value implies that the object can be destroyed accordingly (i.e., ...).