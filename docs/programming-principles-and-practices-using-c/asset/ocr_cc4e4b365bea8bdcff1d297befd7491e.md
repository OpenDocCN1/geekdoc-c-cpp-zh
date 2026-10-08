We use **pair** when we need exactly two elements and don't care to define a specific type. If we need zero or more elements, we can use a **tuple** from `<tuple>`:

```
template <typename... Types>
struct tuple {
    explicit constexpr tuple(const Types& ...);    // construct from N values
    template<typename... Atypes>
    explicit constexpr tuple(const Atypes&& ...); // construct from N values
    // . . . copy and move operations . . .
};

template <class... Types>
constexpr tuple<Types...> make_tuple(Types&&...);      // construct tuple
                                                        // from N values
```

The **tuple** implementation uses a feature beyond the scope of this book, variadic templates. This is what those ellipses (. . .) refer to. However, we can use **tuples** much as we do **pairs**. For example:

```
auto t0 = make_tuple();              // no elements
auto t1 = make_tuple(123.456);       // one element of type double
auto t2 = make_tuple(123.456, 'a');  // two elements of types double and char
auto t3 = make_tuple(12,'a',string{"How?"});  // three elements of types int,
                                               // char, and string
```

A **tuple** can have many elements, so we can't just use **first** and **second** to access them. Instead, a function **get** is used:

```
auto d = get<0>(t1);   // the double
auto n = get<0>(t3);    // the int
auto c = get<1>(t3);    // the char
auto s = get<2>(t3);    // the string
```

The subscript for **get** is provided as a template argument. As can be seen from the example, **tuple** subscripting is zero-based.

Tuples are mostly used in generic programming.

# B.6.4 initializer_list

In `<initializer_list>`, we find the definition of **initializer_list**:

```
template<typename T>
class initializer_list {
```