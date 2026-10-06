# ISO/IEC 14882:2017(E)

1 An object of class stores any instance of type that satisfies the constructor requirements or has no value, and this is referred to as the state of the class object. The stored instance is the contained value. Two states are equivalent if either they have no value, or both have a value and the contained values are equivalent.

2 The non-any_cast functions provide type-safe access to the contained value.
3 Implementations [Example: the object constructed is holding only an int. — example] Such small-object optimization should only be applied to types T for which is_notrow_move_constructible_v<T> is true.

# 23.8.3.1 Construction and destruction [any::cons]

```
constexpr any() noexcept;
1 Postconditions: has_value() is false.
ay(const any other);
2 Effects: If has_value() is false, constructs an object that has no value. Otherwise, equivalent to (any(inplace_type<T>, any_cast<T>&)) where T is the type of the contained value.
3 Throws: Any exception arising from calling the selected constructor for the contained value.
any(any&& other) noexcept;
4 Effects: If has_value() is false, constructs an object that has no value. Otherwise, constructs an object of type that any contains the contained value of other, or an object of the same type constructed from the contained value other considering that value as a value.
5 Postconditions: other is in a valid but otherwise unspecified state.
```

```
template<class T>
any(T&& value);
6 Let: VT shall decay<T>.
7 Requirements: VT shall satisfy the CopyConstructible requirements.
8 Effects: Constructs an object of type that contains an object of type VT direct-initializing as any, if VT is not a specialization of in_place_type_t, and is_copy_constructible_v<VT> is true.
9 Remarks: This constructor shall not participate in overload resolution VT is not the same type as any.
10 Throws: Any exception thrown by the selected constructor of VT.
```

```
template<class T, class... Args>
explicit any(in_place_type<T>, Args&&... args);
11 Let VT be decay<T>.
12 Requirements: VT shall satisfy the CopyConstructible requirements.
13 Effects: Initializes the contained value as direct-initializing an object of type VT with the arguments std::forward<Args>(args) . . . .
14 Postconditions: +this contains a value of type VT.
15 Throws: Any exception thrown by the selected constructor of VT.
16 Remarks: This constructor shall not participate in overload resolution unless is_copy_constructible_v<VT> is true and is_constructible_v<VT, Args...> is true.
```