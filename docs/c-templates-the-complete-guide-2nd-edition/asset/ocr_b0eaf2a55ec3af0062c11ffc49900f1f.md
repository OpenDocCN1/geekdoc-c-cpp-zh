function type that is qualified with `const`, `volatile`, `&`, and/or `&&`).

+   - Provided T is a referenceable type, same as `is_assignable<T&, T&&>::value`, `is_trivially_assignable<T&, T&&>::value`, or `is_nothrow_assignable<T&, T&&>::value` respectively.
+   - Note that `void`, built-in array types, and classes with deleted move-assignment operator cannot be move-assigned.
+   - Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void` or an array of unknown bound.
+   - For example:

[Click here to view code image](#)

```
is_move_assignable_v<int> // yields true
is_move_assignable_v<int&> // yields true
is_move_assignable_v<int&&> // yields true
is_move_assignable_v<void> // yields false
is_move_assignable_v<void*> // yields true
is_move_assignable_v<char[]> // yields false
is_move_assignable_v<std::string> // yields true
is_move_assignable_v<std::unique_ptr<int>> // yields true
```

# `std::is_destructible<T>::value`

`std::is_trivially_destructible<T>::value`

`std::is_nothrow_destructible<T>::value`

+   - Yields `true` if an object of type T can be destroyed (without using a nontrivial operation or with the guarantee that no exception is thrown).
+   - Always yields `true` for references.
+   - Always yields `false` for `void`, array types with unknown bounds, and function types.
+   - `is_trivially_destructible` yields `true` if no destructor of T, any base class, or any nonstatic data member is user-defined or virtual.
+   - Requires that the given type is either complete (see Section 10.3.1 on page 154), (cv-qualified) `void`, or an array of unknown bound.
+   - For example:

[Click here to view code image](#)

```
is_destructible_v<void> // yields false
is_destructible_v<int> // yields true
is_destructible_v<std::string> // yields true
is_destructible_v<std::pair<int,std::string>> // yields true
```