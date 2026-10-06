
# ISO/IEC 14882:2017(E)

```cpp
// 23.2.3, swap
template <class T>
void swap(T&& a, T&& b) noexcept(see below);
template <class T, size_t N>
void swap(T (&)[N], T (&)[N]) noexcept(is_nothrow_swappable_v<T>);
```

```cpp
// 23.2.4, exchange
template <class T, class U = T>
T exchange(T obj, U& new_val);
```

```cpp
// 23.2.5, forward/move
template <class T>
constexpr T&& forward(remove_reference_t<T>&) noexcept;
template <class T>
constexpr T&& forward(remove_reference_t<T>&&) noexcept;
template <class T>
constexpr T move(remove_reference_t<T>&&) noexcept;
template <class T>
constexpr conditional_t<
    !is_nothrow_constructible_v<T> && is_copy_constructible_v<T>, const T&, T&&>
move_if_noexcept(T&&) noexcept;
```

```cpp
// 23.2.6, as
template <class T>
constexpr add_const<T>& as(const T&&) noexcept;
template <class T>
void as_const(const T&&) = delete;
```

```cpp
// 23.2.7, declval
decl::value_reference<T> declval() noexcept; // as unvaluated operand
```

```cpp
// 23.2.8, compile-time sequences
template<class T, T...>
struct integer_sequence;
template<size_t... I...>
using index_sequence = integer_sequence<size_t, I...>;
template<class T, size_t N>
using make_integer_sequence = integer_sequence<T, see below>;
template<size_t N>
using make_index_sequence = make_integer_sequence<size_t, N>;
```

```cpp
template<class T>
using index_sequence_for = make_index_sequence<sizeof(T)>(T>;
```

```cpp
// 23.2.9, template pair
template <class T1, class T2>
struct pair;
```

```cpp
// 23.2.10, pair specialized algorithms
template <class T1, class T2>
constexpr bool operator==(const T1&, const T2&, const T1&, T2&&);
template <class T1, class T2>
constexpr bool operator()({const T1&, T2&&}, const {const T1&, T2&&});
```

```cpp
template <class T1, class T2>
constexpr bool operator!(const pair<T1, T2>&, const pair<T1, T2>&);
template <class T1, class T2>
constexpr bool operator>(const pair<T1, T2>&, const pair<T1, T2>&);
template <class T1, class T2>
constexpr bool operator=(const pair<T1, T2>&, const pair<T1, T2>&);
template <class T1, class T2>
constexpr bool operator<(const pair<T1, T2>&, const pair<T1, T2>&);

template <class T1, class T2>
void swap(pair<T1, T2>& x, pair<T1, T2>& y) noexcept(noexcept(x.swap(y)));

template <class T1, class T2>
constexpr see below make_pair(T1, T2&&);

// 23.4.4. tuple-like access to pair
template <class T> class tuple_size;
template <size_t i, class T> class tuple_element;

template <class T1, class T2> struct tuple_size<pair<T1, T2>>;
template <class T1, class T2> struct tuple_element<0, pair<T1, T2>>;
template <class T1, class T2> struct tuple_element<1, pair<T1, T2>>;
template <size_t i, class T1, class T2>
constexpr tuple_element_t<i, const pair<T1, T2>&> get(const pair<T1, T2>&) noexcept;
template <size_t i, class T1, class T2>
constexpr tuple_element_t<i, pair<T1, T2>&&> get(pair<T1, T2>&&) noexcept;
template <size_t i, class T1, class T2>
constexpr tuple_element_t<i, const pair<T1, T2>&> get(const pair<T1, T2>&) noexcept;
template <class T1, class T2>
constexpr T1& get(pair<T1, T2>&&, int i) noexcept;
template <class T1, class T2>
constexpr T1& get(const pair<T1, T2>&, int i) noexcept;
template <class T1, class T2>
constexpr T2& get(pair<T1, T2>&&, int i) noexcept;
template <class T1, class T2>
constexpr T2& get(const pair<T1, T2>&, int i) noexcept;
template <class T1, class T2>
constexpr T1& get(pair<T1, T2>&&, int i) noexcept;
template <class T1, class T2>
constexpr T1& get(const pair<T1, T2>&, int i) noexcept;
template <class T1, class T2>
constexpr T2& get(pair<T1, T2>&&, int i) noexcept;
template <class T1, class T2>
constexpr T2& get(const pair<T1, T2>&, int i) noexcept;
template <class T1, class T2>
constexpr T2&& get(pair<T1, T2>&&, int i) noexcept;
template <class T1, class T2>
constexpr T2&& get(const pair<T1, T2>&, int i) noexcept;

// 23.4.5. piecewise construction
struct piecewise_construct {
    explicit piecewise_construct() = default;
};

inline piecewise_construct piecewise_construct();
template <class... Types> class tuple; // defined in <tuple> (23.5.2)

// in-place construction
struct in_place_t {
    explicit in_place_t() = default;
};
inline constexpr in_place_t in_place;
template <class T>
struct in_place_type {
    explicit in_place_type(T) = default;
};
template <class T> inline constexpr in_place_type<T> in_place_type(T);
template <size_t I>
struct in_place_index_t {
    explicit in_place_index_t(I) = default;
};
template <size_t I> inline constexpr in_place_index_t<I> in_place_index;

// floating-point format for numerical conversion
enum class chars_format {
    scientific = unspecified,
    fixed = unspecified,
    hex = unspecified,
    general = scientific | fixed
};

// 23.2.8. primitive output conversion
struct to_chars_result {
    char* ptr;
    error_code ec;
};

to_chars_result to_chars(char* first, char* last, see below value, int base = 10);
to_chars_result to_chars(char* first, char* last, float value);
to_chars_result to_chars(char* first, char* last, double value);
to_chars_result to_chars(char* first, char* last, long double value);

to_chars_result to_chars(char* first, char* last, float value,
    chars_format fmt);
to_chars_result to_chars(char* first, char* last, double value,
    chars_format fmt);
to_chars_result to_chars(char* first, char* last, long double value,
    chars_format fmt);

to_chars_result to_chars(char* first, char* last, float value,
    chars_format fmt, int precision);
to_chars_result to_chars(char* first, char* last, double value,
    chars_format fmt, int precision);
to_chars_result to_chars(char* first, char* last, long double value,
    chars_format fmt, int precision);

// 23.2.9. primitive input conversion
struct from_chars_result {
    const char* ptr;
    error_code ec;
};

from_chars_result from_chars(const char* first, const char* last,
              see below value, int base = 10);
from_chars_result from_chars(const char* first, const char* last, float& value,
              chars_format fmt = chars_format::general);
from_chars_result from_chars(const char* first, const char* last, double& value,
              chars_format fmt = chars_format::general);
from_chars_result from_chars(const char* first, const char* last, long double& value,
              chars_format fmt = chars_format::general);
```

1 The header `<utility>` defines several types and function templates that are described in this Clause. It also defines the template pair and various function templates that operate on pair objects.

2 The type `chars_format` is a bitmask ([20.2.4.1]) with elements scientific, fixed, and hex.

## 23.2. Operators [operators]

- 1 To avoid redundant definitions of operator!= out of operator!= and operators >, <=, and out of operator<, the library provides the following:

```cpp
template <class T> bool operator!(const T& x, const T& y);
```
- 2 Requires: Type T is EqualityComparable (Table 20).
- 3 Returns: !(x == y).

```cpp
template <class T> bool operator<(const T& x, const T& y);
```

- 4 Requires: Type T is LessComparable (Table 21).
- 5 Returns: (y < x).

```cpp
template <class T> bool operator<=(const T& x, const T& y);
```

- 6 Requires: Type T is LessThanComparable (Table 21).
- 7 Returns: !(x <= y).

```cpp
template <class T> bool operator>=(const T& x, const T& y);
```

- 8 Requires: Type T is GreaterThanComparable (Table 21).
- 9 Returns: !(x >= y).
