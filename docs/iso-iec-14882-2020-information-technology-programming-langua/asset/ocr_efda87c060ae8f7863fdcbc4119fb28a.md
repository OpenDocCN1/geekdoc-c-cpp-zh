# 20.8.4.5 Observers [any.observers]

```
bool has_value() const noexcept;
```

Returns: true if *this contains an object, otherwise false.

```
const type_info& type() const noexcept;
```

Returns: typeid(T) if *this has a contained value of type T, otherwise typeid(void).

[Note 1: Useful for querying against types known either at compile time or only at runtime. — end note]

# 20.8.5 Non-member functions [any.nonmembers]

```
void swap(any& x, any& y) noexcept;
```

Effects: Equivalent to x.swap(y).

```
template<class T, class... Args>
    any make_any(Args&&... args);
```

Effects: Equivalent to: return any(in_place_type<T>, std::forward<Args>(args)...);

```
template<class T, class U, class... Args>
    any make_any(initializer_list<U> il, Args&&... args);
```

Effects: Equivalent to: return any(in_place_type<T>, il, std::forward<Args>(args)...);

```
template<class T>
    T any_cast(const any& operand);
template<class T>
    T any_cast(any& operand);
template<class T>
    T any_cast(any&& operand);
```

Let U be the type remove_cvref_t<T>.

Mandates: For the first overload, is_constructible_v<T, const U&> is true. For the second overload, is_constructible_v<T, U&> is true. For the third overload, is_constructible_v<T, U> is true.

Returns: For the first and second overload, static_cast<T>(*any_cast<U>(&operand)). For the third overload, static_cast<T>(std::move(*any_cast<U>(&operand))).

Throws: bad_any_cast if operand.type() != typeid(remove_reference_t<T>).

> [Example 1:
>     any x(5); // x holds int
>     assert(any_cast<int>(x) == 5); // cast to value
>     any_cast<int&>(x) = 10; // cast to reference
>     assert(any_cast<int>(x) == 10);
> 
>     x = "Meow"; // x holds const char*
>     assert(strcmp(any_cast<const char*>(x), "Meow") == 0);
>     any_cast<const char*&>(x) = "Harry";
>     assert(strcmp(any_cast<const char*>(x), "Harry") == 0);
> 
>     x = string("Meow"); // x holds string
>     string s, s2("Jane");
>     s = move(any_cast<string&>(x)); // move from any
>     assert(s == "Meow");
>     any_cast<string&>(x) = move(s2); // move to any
>     assert(any_cast<const string&>(x) == "Jane");
> 
>     string cat("Meow");
>     const any y(cat); // const y holds string
>     assert(any_cast<const string&>(y) == cat);
> 
>     any_cast<string&>(y); // error: cannot any_cast away const
>     — end example]