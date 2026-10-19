
```cpp
// 20.7.1.2, hash support
template<class T> struct hash;
template<class... Types> struct hash<variant<Types...>>;
template<> struct hash<monostate>;
}
```

## 20.7.3 Class template variant

### 20.7.3.1 General

```cpp
namespace std {
  template<class... Types>
  class variant {
  public:
    // 20.7.3.2, constructors
    constexpr variant() noexcept(see below);
    constexpr variant(const variant&);
    constexpr variant(variant&&) noexcept(see below);

    template<class T>
      constexpr variant(T&&) noexcept(see below);

    template<class T, class... Args>
      constexpr explicit variant(in_place_type_t<T>, Args&&...);
    template<class T, class U, class... Args>
      constexpr explicit variant(in_place_type_t<T>, initializer_list<U>, Args&&...);

    template<size_t I, class... Args>
      constexpr explicit variant(in_place_index_t<I>, Args&&...);
    template<size_t I, class U, class... Args>
      constexpr explicit variant(in_place_index_t<I>, initializer_list<U>, Args&&...);

    // 20.7.3.3, destructor
    ~variant();

    // 20.7.3.4, assignment
    constexpr variant& operator=(const variant&);
    constexpr variant& operator=(variant&&) noexcept(see below);

    template<class T> variant& operator=(T&&) noexcept(see below);

    // 20.7.3.5, modifiers
    template<class T, class... Args>
      T& emplace(Args&&...);
    template<class T, class U, class... Args>
      T& emplace(initializer_list<U>, Args&&...);
    template<size_t I, class... Args>
      variant_alternative_t<I, variant<Types...>>& emplace(Args&&...);
    template<size_t I, class U, class... Args>
      variant_alternative_t<I, variant<Types...>>& emplace(initializer_list<U>, Args&&...);

    // 20.7.3.6, value status
    constexpr bool valueless_by_exception() const noexcept;
    constexpr size_t index() const noexcept;

    // 20.7.3.7, swap
    void swap(variant&) noexcept(see below);
  };
}
```

¹ Any instance of `variant` at any given time either holds a value of one of its alternative types or holds no value. When an instance of `variant` holds a value of alternative type T, it means that a value of type T, referred to as the variant object’s *contained value*, is allocated within the storage of the variant object. Implementations are not permitted to use additional storage, such as dynamic memory, to allocate the

is ill-formed, as both alternative types have an equally viable constructor for the argument. — end note]

Effects: Initializes *this to hold the alternative type T_j and direct-initializes the contained value as if direct-non-list-initializing it with std::forward<T>(t).

Postconditions: holds_alternative<T_j>(*this) is true.

Throws: Any exception thrown by the initialization of the selected alternative T_j.

Remarks: The expression inside noexcept is equivalent to is_nothrow_constructible_v<T_j, T>. If T_j’s selected constructor is a constexpr constructor, this constructor is a constexpr constructor.

```
template<class T, class... Args> constexpr explicit variant(in_place_type_t<T>, Args&&... args);
```

Constraints:

- There is exactly one occurrence of T in Types... and
- is_constructible_v<T, Args...> is true.

Effects: Initializes the contained value as if direct-non-list-initializing an object of type T with the arguments std::forward<Args>(args)...

Postconditions: holds_alternative<T>(*this) is true.

Throws: Any exception thrown by calling the selected constructor of T.

Remarks: If T’s selected constructor is a constexpr constructor, this constructor is a constexpr constructor.

```
template<class T, class U, class... Args>
constexpr explicit variant(in_place_type_t<T>, initializer_list<U> il, Args&&... args);
```

Constraints:

- There is exactly one occurrence of T in Types... and
- is_constructible_v<T, initializer_list<U>&, Args...> is true.

Effects: Initializes the contained value as if direct-non-list-initializing an object of type T with the arguments il, std::forward<Args>(args)...

Postconditions: holds_alternative<T>(*this) is true.

Throws: Any exception thrown by calling the selected constructor of T.

Remarks: If T’s selected constructor is a constexpr constructor, this constructor is a constexpr constructor.

```
template<size_t I, class... Args> constexpr explicit variant(in_place_index_t<I>, Args&&... args);
```

Constraints:

- I is less than sizeof...(Types) and
- is_constructible_v<T_I, Args...> is true.

Effects: Initializes the contained value as if direct-non-list-initializing an object of type T_I with the arguments std::forward<Args>(args)...

Postconditions: index() is I.

Throws: Any exception thrown by calling the selected constructor of T_I.

Remarks: If T_I’s selected constructor is a constexpr constructor, this constructor is a constexpr constructor.

```
template<size_t I, class U, class... Args>
constexpr explicit variant(in_place_index_t<I>, initializer_list<U> il, Args&&... args);
```

Constraints:

- I is less than sizeof...(Types) and
- is_constructible_v<T_I, initializer_list<U>&, Args...> is true.

Effects: Initializes the contained value as if direct-non-list-initializing an object of type T_I with the arguments il, std::forward<Args>(args)...

*Postconditions:* `index()` is `I`.

*Remarks:* If `T_i`'s selected constructor is a constexpr constructor, this constructor is a constexpr constructor.

### 20.7.3.3 Destructor

`~variant();`

*Effects:* If `valueless_by_exception()` is false, destroys the currently contained value.

*Remarks:* If `is_trivially_destructible_v<T_i>` is true for all `T_i`, then this destructor is trivial.

### 20.7.3.4 Assignment

`constexpr variant& operator=(const variant& rhs);`

Let `j` be `rhs.index()`.

*Effects:*

- — If neither `*this` nor `rhs` holds a value, there is no effect.
- — Otherwise, if `*this` holds a value but `rhs` does not, destroys the value contained in `*this` and sets `*this` to not hold a value.
- — Otherwise, if `index() == j`, assigns the value contained in `rhs` to the value contained in `*this`.
- — Otherwise, if either `is_nothrow_copy_constructible_v<T_j>` is true or `is_nothrow_move_constructible_v<T_j>` is false, equivalent to `emplace<j>(get<j>(rhs))`.
- — Otherwise, equivalent to `operator=(variant(rhs))`.

*Returns:* `*this`.

*Postconditions:* `index() == rhs.index()`.

*Remarks:* This operator is defined as deleted unless `is_copy_constructible_v<T_i> && is_copy_assignable_v<T_i>` is true for all `i`. If `is_trivially_copy_constructible_v<T_i> && is_trivially_copy_assignable_v<T_i> && is_trivially_destructible_v<T_i>` is true for all `i`, this assignment operator is trivial.

`constexpr variant& operator=(variant&& rhs) noexcept(see below);`

Let `j` be `rhs.index()`.

*Constraints:* `is_move_constructible_v<T_i> && is_move_assignable_v<T_i>` is true for all `i`.

*Effects:*

- — If neither `*this` nor `rhs` holds a value, there is no effect.
- — Otherwise, if `*this` holds a value but `rhs` does not, destroys the value contained in `*this` and sets `*this` to not hold a value.
- — Otherwise, if `index() == j`, assigns `get<j>(std::move(rhs))` to the value contained in `*this`.
- — Otherwise, equivalent to `emplace<j>(get<j>(std::move(rhs)))`.

*Returns:* `*this`.

*Remarks:* If `is_trivially_move_constructible_v<T_i> && is_trivially_move_assignable_v<T_i> && is_trivially_destructible_v<T_i>` is true for all `i`, this assignment operator is trivial. The expression inside `noexcept` is equivalent to: `is_nothrow_move_constructible_v<T_i> && is_nothrow_move_assignable_v<T_i>` for all `i`.

- — If an exception is thrown during the call to `T_j`'s move construction (with `j` being `rhs.index()`), the variant will hold no value.
- — If an exception is thrown during the call to `T_j`'s move assignment, the state of the contained value is as defined by the exception safety guarantee of `T_j`'s move assignment; `index()` will be `j`.

`template<class T> variant& operator=(T&& t) noexcept(see below);`

Let `T_j` be a type that is determined as follows: build an imaginary function `FUN(T_i)` for each alternative type `T_i` for which `T_i x[] = {std::forward<T>(t)};` is well-formed for some invented variable `x`. The
