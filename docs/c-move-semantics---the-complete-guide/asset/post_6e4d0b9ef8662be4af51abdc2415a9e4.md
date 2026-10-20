
## 14.3.2 Move Iterators in Constructors and Member Functions

You can also use move iterators wherever an algorithm that reads elements once is used. A useful scenario might be to move elements of a source container to another container (of the same or a different kind). For example:

```cpp
#include <iostream>
#include <string>
#include <list>
#include <vector>

template <typename T>
void print(const std::string& name, const T& coll)
{
    std::cout << name << " (" << coll.size() << " elems): ";
    for (const auto& elem : coll) {
        std::cout << "\"" << elem << "\" ";
    }
    std::cout << "\n";
}

int main()
{
    std::list<std::string> src{"don't", "vote", "for", "liars"};
    // move all elements from the list to the vector:
    std::vector<std::string> vec{std::make_move_iterator(src.begin()),
        std::make_move_iterator(src.end())};
    print("src", src);
    print("vec", vec);
}
```

The program has the following output: ( ? signaling that we do not know the value):

```
src (4 elems): "?" "?" "?" "?"
vec (4 elems): "don't" "vote" "for" "liars"
```

Note that the number of elements in the source container did not change. We moved all elements to the initialized new container. Therefore, the elements in the source range are in a moved-from state afterwards and we do not know their values.

## 14.4 Summary

- The C++ standard library provides special algorithms to move multiple elements, called `std::move()` (same name as the `std::move()` to mark a single object as movable) and `std::move_backward()`. They leave elements in a moved-from state.
- Removing algorithms can leave elements in a moved-from state.
- Move iterators allow us to use move semantics when iterating over elements. You can use these iterators in algorithms or other places such as constructors where ranges are used to initialize/set values. However, ensure that the iterators use each element only once.

## Chapter 15

## Move Semantics in Types of the C++ Standard Library

This chapter discusses the most important or remarkable applications of move semantics in the C++ standard library.

It might help you to better understand basic types such as strings and containers and give you some insights into tricky use of move semantics.

## 15.1 Move Semantics for Strings

Strings are objects that might allocate memory to hold their values. For that reason, you can benefit from using move semantics for them.

We have already had several examples in the book about how strings support move semantics:

- Moving strings into a vector
- Implementing a move constructor for strings
- Initializing string members
- Reading strings in a loop and using them after a move()

In this section, we will present the impact of move semantics on string in more detail.

### 15.1.1 String Assignments and Capacity

The capacity of strings (the memory currently available for the value) does usually not shrink. Only move operations, `swap()`, or `shrink_to_fit()` might shrink the capacity.

Consider the following example:

`lib/stringmoveassign.cpp`

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string s0;
    std::string s1{"short"};
    std::string s2{"a string with an extraordinarily long value"};
    std::cout << "- s0 capa: " << s0.capacity() << " ('" << s0 << "')\n";
    std::cout << "  s1 capa: " << s1.capacity() << " ('" << s1 << "')\n";
    std::cout << "  s2 capa: " << s2.capacity() << " ('" << s2 << "')\n";

    std::string s3{std::move(s1)};
    std::string s4{std::move(s2)};
    std::cout << "- s1 capa: " << s1.capacity() << " ('" << s1 << "')\n";
    std::cout << "  s2 capa: " << s2.capacity() << " ('" << s2 << "')\n";
    std::cout << "  s3 capa: " << s3.capacity() << " ('" << s3 << "')\n";
    std::cout << "  s4 capa: " << s4.capacity() << " ('" << s4 << "')\n";

    std::string s5{"quite a reasonable value"};
    std::cout << "- s4 capa: " << s4.capacity() << " ('" << s4 << "')\n";
    std::cout << "  s5 capa: " << s5.capacity() << " ('" << s5 << "')\n";

    s4 = std::move(s5);
    std::cout << "- s4 capa: " << s4.capacity() << " ('" << s4 << "')\n";
    std::cout << "  s5 capa: " << s5.capacity() << " ('" << s5 << "')\n";
}
```

In this program, you can first see that usually even empty strings have capacity for some characters due to the small string optimization (SSO), which usually reserves 15 or 22 bytes for the value in the string itself. Beyond the size for SSO, the string allocates the memory on the heap, which has at least size necessary to store the value. Therefore, after

```cpp
std::string s0;
std::string s1{"short"};
std::string s2{"a string with an extraordinarily long value"};
```

we might get something like one of the following outputs:

| Platform | `s0` | `s1` | `s2` |
|----------|------|------|------|
| A | `capa: 15 ('')` | `capa: 15 ('short')` | `capa: 43 ('a string with an extraordinarily long value')` |
| B | `capa: 22 ('')` | `capa: 22 ('short')` | `capa: 47 ('a string with an extraordinarily long value')` |

Here, both platforms seem to support SSO (for up to 15 or 22 chars) and the second platform allocates memory for 47 chars when only memory for 43 chars is needed.

On all platforms, a moved-from string is usually empty. This applies even when the value is not stored in externally allocated memory (so that we have to copy all characters). After:

```cpp
std::string s3{std::move(s1)};
std::string s4{std::move(s2)};
```

we usually get something like:

| Variable | Platform A | Platform B |
|----------|------------|------------|
| `s1` | `capa: 15 ('')` | `capa: 22 ('')` |
| `s2` | `capa: 15 ('')` | `capa: 22 ('')` |
| `s3` | `capa: 15 ('short')` | `capa: 22 ('short')` |
| `s4` | `capa: 43 ('a string with an extraordinarily long value')` | `capa: 47 ('a string with an extraordinarily long value')` |

However, note that there is no guarantee that `s1` becomes empty. As usual, the C++ standard library guarantees only that a moved-from string is in a valid but unspecified state, which means that `s1` could still have the value `"short"` or even any other value.

Move assigning a different string value might shrink the capacity. The last two steps of the example program essentially perform:

```cpp
std::string s4{"a string with an extraordinarily long value"};
std::string s5{"quite a reasonable value"};
s4 = std::move(s5);
```

You can find the following outputs in practice:

| Platform behavior | State | `s4` | `s5` |
|---|---|---|---|
| Swapping memory | before move | `capa: 43 ('a string with an extraordinarily long value')` | `capa: 24 ('quite a reasonable value')` |
| Swapping memory | after move | `capa: 24 ('quite a reasonable value')` | `capa: 43 ('')` |
| Moving memory (after freeing the old memory) | before move | `capa: 47 ('a string with an extraordinarily long value')` | `capa: 31 ('quite a reasonable value')` |
| Moving memory (after freeing the old memory) | after move | `capa: 31 ('quite a reasonable value')` | `capa: 22 ('')` |

As you can see, the capacity of `s4` usually shrinks, sometimes to the capacity of the source, sometimes to the minimum capacity for empty strings. However, neither is guaranteed.

## 15.2 Move Semantics for Containers

Containers are usually objects that have to allocate memory to hold their elements. For that reason, you can benefit from using move semantics for them. However, there is one exception: `std::array<>` does not allocate memory on the heap, which means that for `std::array<>` special rules apply.

We have already had several examples in the book about how containers support move semantics. In the initial example motivating move semantics, we saw the following support for move semantics:

- By overloading `push_back()`, the C++ standard supports move semantics for inserting new elements.
- By providing a move constructor and a move assignment operator, containers make copying temporary objects (such as return values) cheap.

That is typical. All containers support move semantics when doing the following:

- Copying the containers
- Assigning the containers
- Inserting elements into the container

However, there is more to say.

### 15.2.1 Basic Move Support for Containers as a Whole

All containers define a move constructor and move assignment operator to support move semantics for unnamed temporary objects and objects marked with `std::move()`.

For example, class `std::list<>` is declared as follows:

```cpp
template<typename T, typename Allocator = allocator<T>>
class list {
public:
    ...
    list(const list&);                // copy constructor
    list(list&&);                     // move constructor
    list& operator=(const list&);     // copy assignment
    list& operator=(list&&) noexcept(...);  // move assignment
    ...
};
```

This makes returning/passing a container by value and assigning the return value cheap. For example:

```cpp
std::list<std::string> createAndInsert()
{
    std::list<std::string> coll;
    ...
    return coll;    // move constructor if not optimized away
}

std::list<std::string> v;
...
v = createAndInsert();  // move assignment
```
