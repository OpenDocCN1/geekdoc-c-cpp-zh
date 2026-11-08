
### `std::is_standard_layout<T>::value`

- an array of such types
- and its cv-qualified versions of those types
- In contrast to `is_trivial`, volatile members are allowed, references are not allowed, members might not have different access, and members might not be distributed among different base classes.
- Requires that the given type (for arrays, the base type) is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

### `std::is_pod<T>::value`

- Yields true if `T` is a POD type (POD).
- Objects of such types can be copied by copying the underlying storage (e.g. using `memcpy()`).
- Same as: `is_trivial<T> && is_standard_layout<T>`.
- Yields false for:
  - classes that don't have a trivial default constructor, copy/move constructor, copy/move assignment, or destructor
  - classes that have virtual members or virtual base classes
  - classes that have volatile or reference members
  - classes that have members in different (base) classes or with different access
  - the types of lambda expressions (called closure types)
  - functions
  - `void`
  - types removed from these types
- Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

### `std::is_literal_type<T>::value`

- Yields true if the given type is a valid pure literal type for a `constexpr` function (which notably excludes any type requiring nontrivial destruction).
- Yields true if `T` is a literal type:
  - a scalar type (integral, float, enum, pointer; see `is_scalar()` on page 707)
  - a reference
  - a class type with at least one `constexpr` constructor that is not a copy/move constructor (in each (base) class, no user-defined or virtual destructor in any (base) class or member, and where every initialization for nonstatic data members is a constant expression)
  - an array of such types
- Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

### `std::is_empty<T>::value`

- Yields true if `T` is a class type but not a union type, whose objects hold no data.
- Yields true if defined as class or struct with:
  - no nonstatic data members other than bit-fields of length 0
  - no virtual member functions
  - no virtual base classes
  - no nonempty base classes
- Requires that given type is complete (see Section 10.3.1 on page 154) if it is a class/struct (an incomplete union is undefined).

### `std::is_polymorphic<T>::value`

- Yields true if `T` is a polymorphic class type (a class that declares or inherits a virtual function).
- Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

### `std::is_abstract<T>::value`

- Yields true if `T` is an abstract class type (a class for which no objects can be created because it has at least one pure virtual member function).
- Requires that the given type is either complete (see Section 10.3.1 on page 154).

### `std::is_final<T>::value`

- Yields true if `T` is a final class type (a class or union that can't serve as a base class in another class).
- For all non-class/union types such as `int`, it returns false (this is because no such type can be final).
- Requires that the given type is either complete (see Section 10.3.1 on page 154) or not a class/struct/union.
- Available since C++14.

### `std::has_virtual_destructor<T>::value`

- Yields true if type `T` has a virtual destructor.
- Requires that given type is complete (see Section 10.3.1 on page 154) if it is a class/struct (an incomplete union is fine).

### `std::has_unique_object_representations<T>::value`

- Yields true if any two objects of type `T` have the same object representation in memory. That is, two identical values are always represented using the same sequence of byte values.
- Objects with this property can produce a reliable hash value by hashing the associated byte sequence (there is no risk that some bits participating in padding in the object representation might differ from one case to another).
- Requires that the given type is trivially copyable (see Section 7.3.1 on page 72) and either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void` or an array of unknown bounds.
- Available since C++17.

### `std::alignment_of<T>::value`

- Yields the alignment value of an object of type `T` as `std::size_t` (for arrays, the element type; for references, the referenced type).
- Same as: `alignof(T)`
- This trait was introduced in C++11 before the `alignof(...)` construct. It is still useful, however, because the trait can be passed around as a class, which is useful for certain metaprograms.
- Requires that `alignof(T)` is a valid expression.
- Use `std::alignment_of<>` to get the common alignment of multiple types (see Section D.9 on page 733).

### `std::rank<T>::value`

- Yields the number of dimensions of an array of type `T` as `std::size_t`.
- Yields 0 for all other types.
- Pointers do not have any associated dimensions. An unspecified bound in an array type does specify a dimension (so, although a function parameter is declared with an array type, it does not have an actual array type, and `std::rank` is not an array type either. See Section 2.1.0 on page 704.)

For example:

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_481_0.png)

```cpp
int a[2][5];
std::rank<decltype(a)>;       // yields 2
std::extent<decltype(a)>;     // yields 2
extern int p[];
std::rank<decltype(p)>;        // yields 1
```

### `std::extent<T>::value`

- Yields the size of the first or each dimension of an array of type `T` as `std::size_t`.
- Yields 0, if it is not an array, the dimension doesn't exist, or the size of the dimension is not known.
- See Section 15.9 on page 655 for implementation details.

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_481_1.png)

```cpp
int a[5][5];
std::extent_v<decltype(a)>;       // yields 5
std::extent_v<decltype(a), 1>;    // yields 5
std::extent_v<decltype(a), 2>;    // yields 0
extern int p[];
std::extent_v<decltype(p)>;        // yields 0
std::extent_v<decltype(p), 1>;     // yields 0
```

### `std::underlying_type<T>::type`

- Yields the underlying type of enum `T`.
- Requires the given type to be a complete enumeration type (see Section 10.3.1 on page 154). For all other types, it has undefined behavior.

### `std::is_invocable<T, Args...>::value` / `std::is_nothrow_invocable<T, Args...>::value`

- `std::is_invocable<T, Args...>::value` yields true if `T` is usable as a callable for `Args...`.
- `std::is_nothrow_invocable<T, Args...>::value` yields true if `T` is usable as a callable for `Args...`, with the guarantee that no exception is thrown.
- That is, we can use these traits to test whether we can call or `std::invoke()` a given callable and its `Args...` (see Section 9.1.1 on page 157 for details about callables and `std::invoke()`).
- Requires that all given types are complete (see Section 10.3.1 on page 154) or (for unqualified `void`) void or an array of unknown bounds.
- For example:

```cpp
return true;
}
};
std::is_invocable_r_v<RET_T, T, Args...>::value    // false
std::is_invocable_r_v<RET_T, T, Args...>::value    // true
std::is_invocable_r_v<RET_T, T, Args...>::value    // false
std::is_invocable_r_v<RET_T, T, Args...>::value    // true
```

### `std::is_invocable_r_v<RET_T, T, Args...>` / `std::is_nothrow_invocable_r_v<RET_T, T, Args...>`

- Available since C++17.
- `std::is_invocable_r_v<RET_T, T, Args...>` yields `true` if we can use `T` as a callable for `Args...`, returning a value convertible to type `RET_T`.
- `std::is_nothrow_invocable_r_v<RET_T, T, Args...>` yields `true` if we can use `T` as a callable for `Args...` with the guarantee that no exception is thrown, returning a value convertible to type `RET_T`.
- That is, we can use these traits to test whether we can call or `std::invoke()` with a specific type of `T`, and use the return value as `RET_T`. (See Section 1.1 on page 57 for details about callables and `std::invoke()`.)
- Requires that all passed types are complete (see Section 13.1.3 on page 354).

For example:

```cpp
struct C {
    bool operator() (int) const {
        return true;
    }
};

std::is_invocable_v<decltype(C{}), int>;                 // true
std::is_invocable_r_v<bool, decltype(C{}), int>;         // true
std::is_invocable_r_v<void, decltype(C{}), int>;         // true
std::is_invocable_r_v<std::string, decltype(C{}), int>;  // false
std::is_nothrow_invocable_r_v<bool, decltype(C{}), int>; // false
std::is_invocable_r_v<int, decltype(C{}), int>;          // true
std::is_invocable_r_v<long, decltype(C{}), int>;         // true
std::is_invocable_r_v<double, decltype(C{}), int>;       // true
std::is_invocable_r_v<const char*, decltype(C{}), int>;  // false
```

### `std::invoke_result<T, Args...>::type` / `std::result_of<T, Args...>::type`

- Yields the return type of the callable `T` called for `Args...`.
- Note that the syntax is slightly different:
  - To invoke `invoke_result`, you have to pass both the type of the callable and the arguments as parameters.
  - To `result_of`, you have to pass a function declaration using the corresponding types.
  - If no call is possible, there is no type member defined, so that using it is an error (which might `SFINAE` out a function template using it in its declaration; see Section 8.4 on page 133).
  - That is, we can use these traits to get the return type obtained when we call `std::invoke()` (the given callable `T` for `Args...`). (See Section 1.1 on page 57 for details about callables and `std::invoke()`.)
  - Requires that all given types are either complete (see Section 13.1.3 on page 354), or (cv-qualified) void, or an array type of unknown bound.
- `invoke_result` is available since C++17 and replaces `result_of`, which is deprecated since C++17, because `invoke_result` provides more improvements and better ensures valid and permitting arbitrary types for `T`.

For example:

```cpp
std::string foo(int);

using R0 = std::result_of_t<decltype(foo)(int)>;       // C++14
using R1 = std::result_of_t<decltype(foo)(int)>;       // C++17
using R2 = std::invoke_result_t<decltype(foo), int>;   // C++17

struct A {
    int operator() (int) const {
        return 0;
    }
};

using R1 = std::invoke_result_t<A&(int)>;              // C++17
using R2 = std::invoke_result_t<A&, int>;               // C++17
```
