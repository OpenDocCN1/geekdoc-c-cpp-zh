# ISO/IEC 14882:2020(E)

of T's copy assignment. This operator is defined as deleted unless is_copy_constructible_v<T> is true and is_copy_assignable_v<T> is true. If is_trivially_copy_constructible_v<T> && is_trivially_copy_assignable_v<T> && is_trivially_destructible_v<T> is true, this assignment operator is trivial.

```
constexpr optional& operator=(optional&& rhs) noexcept(see below);
```

Constraints: is_move_constructible_v<T> is true and is_move_assignable_v<T> is true.

Effects: See Table 43. The result of the expression bool(rhs) remains unchanged.

Table 43: optional::operator=(optional&&) effects [tab:optional.assign.move]

|  | *this contains a value | *this does not contain a value |
|---|---|---|
| rhs contains a value | assigns std::move(*rhs) to the contained value | initializes the contained value as if direct-non-list-initializing an object of type T with std::move(*rhs) |
| rhs does not contain a value | destroys the contained value by calling val->T::~T() | no effect |

Postconditions: bool(rhs) == bool(*this).

Returns: *this.

Remarks: The expression inside noexcept is equivalent to:

```
is_nothrow_move_assignable_v<T> && is_nothrow_move_constructible_v<T>
```

If any exception is thrown, the result of the expression bool(*this) remains unchanged. If an exception is thrown during the call to T's move constructor, the state of *rhs.val is determined by the exception safety guarantee of T's move constructor. If an exception is thrown during the call to T's move assignment, the state of *val and *rhs.val is determined by the exception safety guarantee of T's move assignment. If is_trivially_move_constructible_v<T> && is_trivially_move_assignable_v<T> && is_trivially_destructible_v<T> is true, this assignment operator is trivial.

```
template<class U = T> optional<T>& operator=(U&& v);
```

Constraints: is_same_v<remove_cvref_t<U>, optional> is false, conjunction_v<is_scalar<T>, is_same<T, decay_t<U>>> is false, is_constructible_v<T, U> is true, and is_assignable_v<T&, U> is true.

Effects: If *this contains a value, assigns std::forward<U>(v) to the contained value; otherwise initializes the contained value as if direct-non-list-initializing object of type T with std::forward<U>(v).

Postconditions: *this contains a value.

Returns: *this.

Remarks: If any exception is thrown, the result of the expression bool(*this) remains unchanged. If an exception is thrown during the call to T's constructor, the state of v is determined by the exception safety guarantee of T's constructor. If an exception is thrown during the call to T's assignment, the state of *val and v is determined by the exception safety guarantee of T's assignment.

```
template<class U> optional<T>& operator=(const optional<U>& rhs);
```

Constraints:

+   - is_constructible_v<T, const U&> is true,
+   - is_assignable_v<T&, const U&> is true,
+   - is_constructible_v<T, optional<U>&> is false,
+   - is_constructible_v<T, optional<U>&&> is false,
+   - is_constructible_v<T, const optional<U>&> is false,
+   - is_constructible_v<T, const optional<U>&&> is false,