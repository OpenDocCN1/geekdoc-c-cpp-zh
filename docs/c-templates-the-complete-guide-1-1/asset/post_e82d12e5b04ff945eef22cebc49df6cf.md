
```cpp
std::forward_iterator_tag;
```

With that, `std::iterator_traits<>` assumes `InputIterator<T>`, and we can now overload templates constrained for both iterator categories.

## E.4 CONCEPT TIPS

Although C++ concepts have been worked on for many years now, and experimental implementations have been available in some form for over a decade, broad experience with them is just starting to emerge. We hope that a future edition of this book will be able to provide much more practical guidance about how to design constrained template libraries. Meanwhile, however, we offer three observations.

### E.4.1 Testing Concepts

Concepts are Boolean predicates that are valid constant-expressions. Therefore, given a concept C and some types T1, T2, ..., that model the concept, we can statically assert that observation:

*Click here to view code image*

```cpp
static_assert(C<T1, T2, ...>, "model failure");
```

When designing concepts, it is therefore recommended to also design some types that test them in this way. That includes types that push the boundaries of what the concept entails, answering questions such as the following:

- Do interfaces and/or algorithms need to copy and/or move objects of the types being modeled?
- What conversions are acceptable? Which ones are needed?
- Is the basic set of operations assumed by the template unique? For example, can a type's operators be `++` or `--`?

Here, too, the notion of archetypes (see Section 18.3 on page 653) can be useful.

### E.4.2 Concept Granularity

With concepts becoming part of the C++ language, it is natural to want to build "libraries of concepts," just as we build class libraries and template libraries as soon as those features were available. As with other libraries, it is also natural to want to favor our concepts in various ways. We briefly discussed the example of iterator categories, and it's not a great leap to envision that we could build "range categories" alongside these and perhaps "sequence concepts" on top of those, and so on.

On the other hand, we might be tempted to build all of those concepts on top of "elementary syntax" concepts. For example, we could imagine:

*Click here to view code image*

```cpp
template<typename T>
concept Addable =
  requires (T a, T b) {
    a + b;
  };
```

That is not recommended, however, because it is a concept that has no other semantic connotation, and disparate types will satisfy it. For example, it is satisfied when `T` and `U` are both `std::string` or when one type is a pointer and the other an integral type, and of course with arithmetic types. Yet in those three cases, the notion of Addable means something fundamentally different (respectively, concatenation, iterator displacement, and variants of arithmetic addition). Introducing such a concept is therefore a recipe for libraries with fairly interesting and likely to trigger odd ambiguities.

Instead, it appears that concepts are best designed to model real semantic notions that are in the problem domain. Doing so in a disciplined fashion is bound to improve the overall design of our libraries, as it will bring intrinsically and clearly to the interfaces presented to our clients.

### E.4.3 Binary Compatibility

Experienced C++ programmers are aware that when certain entities (functions and member functions in particular) are compiled down to low-level machine code, a name is associated with them that combines the declared name with the type and scope of the entity. This name, commonly referred to as the mangled name of the entity, is what is used by object code linkers to resolve references to the entity (e.g., from other object files). For example, the mangled name of a function defined as

*Click here to view code image*

```cpp
template<typename T>
concept HasPlus = requires(T a, T b) {
    a + b;
};

template<typename T>
int f(T a) requires HasPlus<T> {
    std::cout << "T\n";
}

void g()
{
    int a, b;
    f(a);
    f(b);
}
```

[Click here to view code image](#)

```cpp
#include <iostream>

template<typename T>
concept HasPlus = requires(T a, T b) {
    a * b;
};

template<typename T>
int f(T a) requires HasPlus<T> {
    std::cout << "T\n";
}

template <int I>
void g() {
    f(I);
}
```

This program must output

```
T
T
```

which means that the two definitions of f() must be mangled differently.

1. Contiguous iterators are a refinement of random access iterators introduced in C++17. No `std::contiguous_iterator` tag was added for them because existing algorithms that rely on `std::ranges::contiguous_range` would be harder to extend if that tag were changed.
2. The specification being proposed for standardization is a little more powerful than this. It breaks down containers into sets of "domain concepts" (including the point of regular expressions and analyses that are sent to one or are clearly a direct subset of the other).
3. The experimental implementation of concepts in GCC 7.1 is known to be deficient in this respect.

# Code Snippets

```cpp
template<typename T> requires LessThanComparable<T>
T max(T a, T b) {
    return a > b ? a : b;
}
```

```cpp
requires LessThanComparable<T>
```

```cpp
class Person
{
private:
    std::string name;
public:
    template <typename T>
    explicit Person(T&& str)
        : name(std::forward<T>(str)) {
            std::cout << "EMPL constructor for " << name << "\n";
        }
};
```

```cpp
template<typename Seq>
    requires Sequence<Seq>
class Sequence
{
public:
    using value_type = typename Seq::value_type;
    Sequence(Seq value) : value_(value) {}

    bool contains(const value_type& val) const {
        return std::find(begin(), end(), val);
    }
};
```

```cpp
template<typename T>
    requires Integral<T> ||
             FloatingPoint<T>
T power(T b, T p);
```

```cpp
template<typename T, typename U>
requires SomeConcept<T, U>
auto f(T x, U y) -> decltype(x+y);
```

```cpp
template<LessThanComparable T>
T max(T a, T b) {
    return b < a ? a : b;
}
```

```cpp
template<typename Seq>
requires EqualityComparable<Seq::value_type>
typename Seq::iterator find(Seq const& seq,
                            typename Seq::value_type const& val)
{
    return std::find(seq.begin(), seq.end(), val);
}
```

```cpp
template<typename T> concept LessThanComparable = ...;
```

```cpp
template<typename T>
concept LessThanComparable = requires(T x, T y) {
    { x < y } -> Bool;
};
```

```cpp
{ x < y } -> bool;
```

```cpp
template<typename T>
concept Swappable = requires(T x, T y) {
  swap(x, y);
};
```

```cpp
...
typename IteratorFor<Seq>;
...
```

```cpp
template<typename Seq>
concept Sequence = requires(Seq seq) {
    typename Seq::iterator;
    requires Iterator<decltype(seq.iterator)>;
    { seq.begin() } -> Seq::iterator;
};
```

```c
int main()
{
    printf(1);        // selects template #1
    printf("1%s");    // selects template #2
}
```

```cpp
template<typename T>
    concept ForwardIterator = ...;
```

```cpp
template<typename T>
concept BidirectionalIterator =
  ForwardIterator<T> &&
  requires (T it) {
    { --it } -> T&;
  };
```

```cpp
template<ForwardIterator T, typename D>
void advance(T& it, D n)
{
    assert(n >= 0);
    for (; n != 0; --n) { ++it; }
}

template<BidirectionalIterator T, typename D>
void advance(T& it, D n)
{
    if (n > 0) {
        for (; n != 0; --n) { ++it; }
    } else if (n < 0) {
        for (; n != 0; ++n) { --it; }
    }
}
```

```cpp
template<typename T>
concept ForwardIterator =
    std::input_iterator<T> &&
    requires {
        typename std::iterator_traits<T>::iterator_category;
        std::is_base_of_v<std::forward_iterator_tag,
                          typename std::iterator_traits<T>::iterator_category>;
    };
```
