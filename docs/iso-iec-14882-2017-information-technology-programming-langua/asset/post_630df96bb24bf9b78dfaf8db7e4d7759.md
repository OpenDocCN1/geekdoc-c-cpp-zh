
# ISO/IEC 14882:2017(E)

constructor. This constructor shall not participate in overload resolution unless is_constructible_v<T, U&> is true, is_name_v<decay_t<U>, in_place_t> is false, and is_same_v<decay_t<U>> is false. The constructor is explicit if and only if is_convertible_v<U&, T> is false.

```cpp
template <class U> explicit(const optional<U> rhs);
```

Effects: If rhs contains a value, the contained value is assigned if direct-initializing an object of type T with the expression *rhs.

Postconditions: bool(rhs) == *(this).

Throws: Any exception thrown by the selected constructor of T.

Remarks: This constructor shall not participate in overload resolution (Note: the OCR text seems to be cut off or repeated here)

- (27.1) — is_constructible_v<T, const U> is true.
- (27.2) — is_constructible_v<T, optional<U>&> is false.
- (27.3) — is_constructible_v<T, optional<U>> is false.
- (27.4) — is_constructible_v<T, const optional<U>> is false,
- (27.5) — is_constructible_v<T, const optional<U>&> is false,
- (27.6) — is_convertible_v<optional<U>&, T> is false.
- (27.7) — is_convertible_v<optional<U>&&, T> is false.
- (27.8) — is_convertible_v<const optional<U>&, T> is false.
- (27.9) — is_convertible_v<const optional<U>&&, T> is false.

The constructor is explicit if and only if is_convertible_v<const U&, T> is false.

```cpp
template <class U> explicit(const optional<U> rhs);
```

Effects: If rhs contains a value, the contained value is assigned if direct-initializing an object of type T with the expression move(*rhs). bool(rhs) is unchanged.

Postconditions: bool(rhs) == *(this).

Throws: Any exception thrown by the selected constructor of T.

Remarks: This constructor shall not participate in overload resolution

- (31.1) — is_constructible_v<T, U&> is true,
- (31.2) — is_constructible_v<T, optional<U>&> is false.
- (31.3) — is_constructible_v<T, optional<U>> is false.
- (31.4) — is_constructible_v<T, const optional<U>> is false,
- (31.5) — is_constructible_v<T, const optional<U>&> is false,
- (31.6) — is_convertible_v<optional<U>&, T> is false,
- (31.7) — is_convertible_v<optional<U>&&, T> is false,
- (31.8) — is_convertible_v<const optional<U>&, T> is false,
- (31.9) — is_convertible_v<const optional<U>&&, T> is false.

The constructor is explicit if and only if is_convertible_v<const U&, T> is false.

## 23.6.3.2 Destructor [optional.dtor]

- optional(U);

Effects: If is trivially_destructible_v<T> == true and *this contains a value, calls val->T::~T()

Remarks: If is_trivially_destructible_v<T> == true then this destructor shall be a trivial destructor.

## 23.6.3.3 Assignment [optional.assign]

optional<T>& operator=(nullopt_t) noexcept;

Effects: *this contains a value, val->T::~T() to destroy the contained value; otherwise no effect.

Returns: *this.

Postconditions: *this does not contain a value.

optional<T>& operator=(const optional& rhs);

Effects: See Table 35.

| Table 35 — optional::operator=(const optional& rhs) effects | *this contains a value | *this does not contain a value |
| :--- | :--- | :--- |
| rhs contains a value | assigns *rhs to the contained value | initializes the contained value as if-direct-non-list-initializing an object of type T with *rhs |
| rhs does not contain a value | destroys the contained value by calling val->T::~T() | no effect |

Returns: *this.

Postconditions: bool(rhs) == bool(*this) remains.

Remarks: If an exception is thrown, the result of the expression bool(*this) remains unchanged. If an exception is thrown during the call to T's copy constructor, no effect. The state of the contained value is as defined by the exception guarantee of T's copy assignment, shall be valid unless copy_constructible_v<T> is true and is_assignable_v<T> is true.

optional<T>& operator=(optional& rhs) noexcept(bool(rhs)) remains unchanged.

Effects: See Table 36.

| Table 36 — optional::operator=(optional& rhs) effects | *this contains a value | *this does not contain a value |
| :--- | :--- | :--- |
| rhs contains a value | assigns std::move(*rhs) to the contained value | initializes the contained value as if-direct-non-list-initializing an object of type T with std::move(*rhs) |
| rhs does not contain a value | destroys the contained value by calling val->T::~T() | no effect |

Returns: *this.

Postconditions: bool(rhs) == bool(*this).

Remarks: The exception is noexcept equivalent to: is_throw_move_assignable<T> && is_throw_move_constructible<T>. If any exception is thrown, the result of the expression bool(*this) remains unchanged. If an exception is thrown during the call to T's move constructor, the state of *rhs.val is determined by the exception guarantee of T. If an exception is thrown during the call to T's move assignment, the state is determined by the exception guarantee of T. This operator shall not participate in overload resolution unless is_constructible<T> is true and is_assignable<T> is true.

```cpp
template <class U> optional<T>& operator=(U&& u);
```

Effects: If this contains a value, std::forward(u) to the contained value; initializes the contained value as if-direct-non-initializing an object of type T with std::forward(u).

Returns: *this.

Postconditions: *this contains a value.

Remarks: If any exception is thrown, the result of the expression bool(*this) remains unchanged. If an exception is thrown during the call to T's constructor, the state of *rhs.val is determined by the exception guarantee of T. If an exception is thrown during the call to T's assignment, the state of *rhs.val is determined by the exception guarantee of T. This function shall not participate in overload resolution unless is_constructible<T, const U&> is true, is_assignable<T, const U&> is true, is_constructible<T, optional<U>&> is false.

```cpp
template <class U> optional<T>& operator=(const optional<U>& rhs);
```

Effects: See Table 37. (Note: Table 37 is missing in provided OCR, but Table 38 is present)

| Table 38 — operator=:operator*(optional<U> rhs) effects | *this contains a value | *this does not contain a value |
| :--- | :--- | :--- |
| rhs contains a value | assigns std::move(*rhs) to the contained value | initializes the contained value as if direct-list-initializing an object of type T with std::move(*rhs) |
| rhs does not contain a value | destroys the contained value by calling val(*T):~T() | no effect |

Returns: *this.

Postconditions: bool(*rhs) == (*this).

Remarks: If any exception is thrown during the call to T's constructor, the state of the expression (*this) remains unchanged. If an exception is thrown during the call to T's exception safety guarantee, the state of *rhs and *rhs.val is determined by the exception guarantee of T. This assignment will not participate in order resolution undefined.

- (24.1) — is_constructible_v<T, U> is true.
- (24.2) — is_assignable_v<optional<U>, T> is true.
- (24.3) — is_constructible_v<T, optional<U>> is false.
- (24.4) — is_assignable_v<optional<U>, T> is false.
- (24.5) — is_constructible_v<T, const optional<U>> is false.
- (24.6) — is_assignible_v<T, const optional<U>> is false.
- (24.7) — is_convertible_v<optional<U>, T> is false.
- (24.8) — is_convertible_v<optional<U>, T> is false.
- (24.9) — is_convertible_v<const optional<U>, T> is false.
- (24.10) — is_convertible_v<const optional<U>, T> is false.
- (24.11) — is_assignable_v<T, optional<U>> is false.
- (24.12) — is_assignable_v<optional<U>, T> is false.
- (24.13) — is_assignable_v<optional<U>, const optional<U>> is false.
- (24.14) — is_assignable_v<const optional<U>, optional<U>> is false.

```cpp
template <class U> operator=(optional<U> rhs); result of the expression (*rhs) remains unchanged.
```

21 Effects: See Table 38.
