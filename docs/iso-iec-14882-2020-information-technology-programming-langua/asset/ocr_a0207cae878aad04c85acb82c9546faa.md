# 17.10 Initializer lists [support.initlist]

# 17.10.1 General [support.initlist.general]

1 The header <initializer_list> defines a class template and several support functions related to list-initialization (see 9.4.5). All functions specified in 17.10 are signal-safe (17.13.5).

# 17.10.2 Header <initializer_list> synopsis [initializer.list.syn]

```
namespace std {
template<class E> class initializer_list {
public:
using value_type = E;
using reference = const E&;
using const_reference = const E&;
using size_type = size_t;
using iterator = const E*;
using const_iterator = const E*;
constexpr initializer_list() noexcept;
constexpr size_t size() const noexcept; // number of elements
constexpr const E* begin() const noexcept; // first element
constexpr const E* end() const noexcept; // one past the last element
};
// 17.10.5, initializer list range access
template<class E> constexpr const E* begin(initializer_list<E> il) noexcept;
template<class E> constexpr const E* end(initializer_list<E> il) noexcept;
}
```

1 An object of type initializer_list<E> provides access to an array of objects of type const E.

> [Note 1: A pair of pointers or a pointer plus a length would be obvious representations for initializer_list. initializer_list is used to implement initializer lists as specified in 9.4.5. Copying an initializer list does not copy the underlying elements. — end note]

2 If an explicit specialization or partial specialization of initializer_list is declared, the program is ill-formed.

```
[[noreturn]] void rethrow_nested() const;
Effects: If nested_ptr() returns a null pointer, the function calls the function std::terminate. Otherwise, it throws the stored exception captured by *this.
```

```
exception_ptr nested_ptr() const noexcept;
Returns: The stored exception captured by this nested_exception object.
```

```
template<class T> [[noreturn]] void throw_with_nested(T&& t);
Let U be decay_t<T>.
Preconditions: U meets the Cpp17CopyConstructible requirements.
Throws: If is_class_v<U> && !is_final_v<U> && !is_base_of_v<nested_exception, U> is true, an exception of unspecified type that is publicly derived from both U and nested_exception and constructed from std::forward<T>(t), otherwise std::forward<T>(t).
```

```
template<class E> void rethrow_if_nested(const E& e);
Effects: If E is not a polymorphic class type, or if nested_exception is an inaccessible or ambiguous base class of E, there is no effect. Otherwise, performs:
if (auto p = dynamic_cast<const nested_exception*>(addressof(e)))
p->rethrow_nested();
```