
```cpp
// insert a copy of elem:
void push_back(const T& elem);

// insert elem when the value of elem is no longer needed:
void push_back(T&& elem);
};
...
```

The `push_back()` function for rvalues forwards the passed element with `std::move()` so that the move constructor of the element type is called instead of the copy constructor.

In the same way, all containers have corresponding overloads. For example:

```cpp
template<typename Key, typename T, typename Compare = less<Key>,
         typename Allocator = allocator<pair<const Key, T>>>
class map {
  public:
    ...
    pair<iterator, bool> insert(const value_type& x);
    pair<iterator, bool> insert(value_type&& x);
    ...
};
```

### Emplace Functions

Since C++11, containers also provide emplace functions (such as `emplace_back()` for vectors). Instead of passing a single argument of the element type (or convertible to the element type), you can pass multiple arguments to initialize a new element directly in the container. That way you save a copy or move.

Note that even then, containers can benefit from move semantics by supporting move semantics for the initial arguments of constructors.

Functions like `emplace_back()` use perfect forwarding to avoid creating copies of the passed arguments. For example, for `std::vector<>`, the `emplace_back()` member function is defined as follows:

```cpp
template<typename T, typename Allocator = allocator<T>>
class vector {
  public:
    ...
    // insert a new element with perfectly forwarded arguments:
    template<typename... Args>
    constexpr T& emplace_back(Args&&... args) {
      ...
      // call the constructor with the perfectly forwarded arguments:
      place_element_in_memory(T(std::forward<Args>(args)...));
      ...
    }
    ...
};
```

Internally, the vector initializes the new element with the perfectly forwarded arguments.

## 15.2.3 Move Semantics for `std::array<>`

`std::array<>` is the only container that does not allocate memory on the heap. In fact, it is implemented as a templated C data structure with an array member:

```cpp
template<typename T, size_t N>
struct array {
  T elems[N];
  ...
};
```

Therefore, we cannot implement move operations in a way that they move pointers to internal memory.

As a consequence, `std::array<>` has a couple of different guarantees:

- The move constructor has linear complexity because it has to move element by element.
- The move assignment operator might always throw because it has to move-assign element by element.

Therefore, in principle, there is no difference between copying or moving an array of numeric values:

```cpp
std::array<double, 1000> arr;
...
auto arr2{arr};                 // copies all double elements/values
auto arr3{std::move(arr)};       // still copies all double elements/values
```

For all other containers, the latter would only move internal pointers to the new object and would therefore be a significantly cheaper operation.

However, moving an array is still better than copying if moving the elements is cheaper than copying them. For example:

```cpp
std::array<std::string, 1000> arr;
...
auto arr2{arr};                 // copies string by string
auto arr3{std::move(arr)};       // moves string by string
```

If the strings allocate heap memory (i.e., they have a significant size if the small string optimization (SSO) is used), moving the array of strings is usually significantly faster.

You can see this with the program `lib/contmove.cpp`, which checks the difference between copying and moving an array and a vector of different element types (double, a small string, and a large string). Note that on your platform, there might still be small performance differences between copying and moving an array of doubles or small strings because slightly different code with different optimizations is generated.

## 15.3 Move Semantics for Vocabulary Types

The C++ standard library provides a couple of vocabulary types for handling one or multiple values with value semantics (objects hold and copy their value autonomously and as a whole).

In principle, they all provide move semantics. However, some of them need special discussion and remarks.

### 15.3.1 Move Semantics for Pairs

`std::pair<>` is a good example of both the benefits of move semantics and the complexity it might introduce. In principle, we have only a generic data structure with two members (defined in namespace `std`):

```cpp
template<typename T1, typename T2>
struct pair {
    T1 first;
    T2 second;
    ...
};
```

However, to support move semantics (and a couple of other tricky corner cases, such as reference members), we have the following declaration here. I show the C++14 version, which I made a bit more readable:

```cpp
template<typename T1, typename T2>
struct pair {
    // types of each member:
    using first_type = T1;       // same as: typedef T1 first_type
    using second_type = T2;
    // the members:
    T1 first;
    T2 second;

    // constructors:
    constexpr pair();
    constexpr pair(const T1& x, const T2& y);
    template<typename U, typename V> constexpr pair(U&& x, V&& y);
    pair(const pair&) = default;
    pair(pair&&) = default;
    template<typename U, typename V> constexpr pair(const pair<U, V>& p);
    template<typename U, typename V> pair& operator=(const pair<U, V>& p);
    template<typename... Args1, typename... Args2>
      pair(piecewise_construct_t, tuple<Args1...> first_args,
           tuple<Args2...> second_args);

    // assignments:
    pair& operator=(const pair& p);
    pair& operator=(pair&& p) noexcept(...);
    template<typename U, typename V> pair& operator=(const pair<U, V>& p);
    template<typename U, typename V> pair& operator=(pair<U, V>&& p);

    // other:
    void swap(pair& p) noexcept(...);
};
```

As you can see, the class supports move semantics. We have a defaulted move constructor and an implemented move assignment operator (which has a corresponding `noexcept` condition not to throw if both member types guarantee not to throw):

```cpp
template<typename T1, typename T2>
struct pair {
    ...
    pair(pair&&) = default;
    ...
    pair& operator=(pair&& p) noexcept(...);
};
```

Therefore, the following code:

```cpp
std::pair<std::string, std::string> p1{"some value", "some other value"};
auto p2{p1};
auto p3{std::move(p1)};

std::cout << "p1: " << p1.first << '/' << p1.second << '\n';
std::cout << "p2: " << p2.first << '/' << p2.second << '\n';
std::cout << "p3: " << p3.first << '/' << p3.second << '\n';
```

has the following output:

```
p1: /
p2: some value/some other value
p3: some value/some other value
```

However, type `std::pair<>` also supports perfect forwarding by dealing with universal/forwarding references:

```cpp
template<typename T1, typename T2>
struct pair {
    ...
    template<typename U, typename V> constexpr pair(U&& x, V&& y);
    ...
};
```

Therefore, we can use move semantics when initializing a pair. For example:

```cpp
int val = 42;
std::string s1{"value of s1"};
std::pair<std::string, std::string> p4{std::to_string(val), std::move(s1)};

std::cout << "s1: " << s1 << '\n';
std::cout << "p4: " << p4.first << '/' << p4.second << '\n';
```

has the following output:

```
s1:
p4: 42/value of s1
```

The corresponding member template is implemented as you would expect for universal/forwarding references:

```cpp
template<typename U, typename V>
constexpr pair::pair(U&& x, V&& y)
    : first(std::forward<U>(x)), second(std::forward<V>(y)) {
}
```

Note that the universal/forwarding references also mean that we can create and assign pairs of different types provided a corresponding type conversion is provided. For example:

```cpp
std::pair<const char*, std::string> p5{"answer", "is 42"};
auto p6{std::move(p5)};

std::cout << "p5: " << p5.first << '/' << p5.second << '\n';
std::cout << "p6: " << p6.first << '/' << p6.second << '\n';
```

has the following output:

```
p5: answer/is 42
p6: answer/is 42
```

When initializing `p6`, we convert the first member of `p5` (declared as `const char*`) to a `std::string`, while using move semantics when using the second member of `p5` to initialize the second member of `p6`.

Finally, note that `std::pair<>` supports members that have reference types. In this case, special rules apply when using `std::move()` for these members. See `basics/members.cpp` for a complete example.

### `std::make_pair()`

`std::pair<>` comes with a convenience function template `std::make_pair<>` for creating pairs without having to specify the types of the members:

```cpp
auto p{std::make_pair(42, "hello")};  // creates std::pair<int, const char*>
```

`std::make_pair<>` is a good example to demonstrate one additional thing you have to take into account when using move semantics with rvalues and universal/forwarding references. Its declaration has changed through the different versions of the C++ standard:

- In the first C++ standard, C++98, `make_pair<>` was declared inside namespace `std` using call-by-reference to avoid unnecessary copying:

```cpp
template<typename T1, typename T2>
pair<T1, T2> make_pair(const T1& a, const T2& b)
{
    return pair<T1, T2>(a, b);
}
```

This, however, almost immediately caused significant problems when using pairs of string literals or raw arrays. For example, when `"hello"` was passed as the second argument, the type of the corresponding
