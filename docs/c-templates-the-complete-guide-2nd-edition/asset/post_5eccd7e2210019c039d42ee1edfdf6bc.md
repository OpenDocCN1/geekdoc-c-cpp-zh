
and member functions in particular) are compiled down to low-level machine code, a name is associated with them that combines the declared name with the type and scope of the entity. This name, commonly referred to as the *mangled name* of the entity, is what is used by the object code linker to resolve references to the entity (e.g., from other object files). For example, the mangled name of a function defined as

```cpp
namespace X {
void f() {}
}
```

is `_ZN1X1fEv` in the Itanium C++ ABI [*ItaniumABI*] (the letters X and f in this encoding come from the namespace name and function name, respectively).

Mangled names cannot “collide” within a program. Therefore, if two functions can potentially coexist in a program, they *must* have distinct mangled names. That, in turn, means that constraints must be encoded in the function name (because template specializations that are identical in every way except their constraints and their function body can appear in different translation units). Consider the following two translation units:

```cpp
#include <iostream>

template<typename T>
concept HasPlus = requires (T x, T y) {
x+y;
};

template<typename T> int f(T p) requires HasPlus<T> {
std::cout << "TU1\n";
}

void g();

int main() {
f(1);
g();
}
```

and

```cpp
#include <iostream>

template<typename T>
concept HasMult = requires (T x, T y) {
x*y;
};

template<typename T> int f(T p) requires HasMult<T> {
std::cout << "TU2\n";
}

template int f(int);

void g() {
f(2);
}
```

This program must output

```
TU1
TU2
```

which means that the two definitions of `f()` must be mangled differently.³

¹ *Contiguous iterators* are a refinement of *random access iterators* introduced in C++17. No `std::contiguous_iterator_tag` was added for them because existing algorithms that rely on `std::random_access_iterator_tag` would no longer be selected if the tag were changed.

² The specification being proposed for standardization is a little more powerful than this. It breaks down constraints into sets of “atomic components” (including the parts of requires expressions) and analyzes those sets to see if one is clearly a strict subset of the other.

³ The experimental implementation of concepts in GCC 7.1 is known to be deficient in this respect.

```cpp
template<typename T> requires LessThanComparable<T>
T max(T a, T b) {
    return b < a ? a : b;
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
        template<typename STR>
        requires std::is_convertible_v<STR,std::string>
        explicit Person(STR&& n)
            : name(std::forward<STR>(n)) {
                std::cout << "TMPL-CONSTR for '" << name << "'\n";
            }
        ...
};
```

```cpp
template<typename Seq>
    requires Sequence<Seq> &&
             EqualityComparable<typename Seq::value_type>
typename Seq::iterator find(Seq const& seq,
                            typename Seq::value_type const& val)
{
    return std::find(seq.begin(), seq.end(), val);
}
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
template<Sequence Seq>
    requires EqualityComparable<typename Seq::value_type>
typename Seq::iterator find(Seq const& seq,
                        typename Seq::value_type const& val)
{
    return std::find(seq.begin(), seq.end(), val);
}
```

```cpp
template<typename T> concept LessThanComparable = ... ;
```

```cpp
template<typename T>
concept LessThanComparable = requires(T x, T y) {
    { x < y } -> bool;
};
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
    requires Iterator<typename Seq::iterator>;
    { seq.begin() } -> Seq::iterator;
    ...
};
```

```cpp
template<IntegerLike T> void print(T val);  //#1
template<StringLike T> void print(T val);  //#2
```

```cpp
int main()
{
    print(1);        // selects template #1
    print("1");     // selects template #2
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
    void advanceIter(T& it, D n)
    {
        assert(n >= 0);
        for (; n != 0; --n) { ++it; }
    }

template<BidirectionalIterator T, typename D>
    void advanceIter(T& it, D n)
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
    InputIterator<T> &&
    requires {
      typename std::iterator_traits<T>::iterator_category;
      std::is_convertible_v<std::iterator_traits<T>::iterator_category,
          std::forward_iterator_tag>;
    };
```

```cpp
static_assert(C<T1, T2, ...>, "Model failure");
```

```cpp
template<typename T, typename U>
concept Addable =
  requires (T x, U y) {
    x + y;
  };
```

```cpp
namespace X {
    void f() {}
}
```

```cpp
#include <iostream>

template<typename T>
concept HasPlus = requires (T x, T y) {
    x+y;
};
template<typename T> int f(T p) requires HasPlus<T> {
    std::cout << "TU1\n";
}

void g();

int main() {
    f(1);
    g();
}
```

```cpp
#include <iostream>

template<typename T>
concept HasMult = requires (T x, T y) {
    x*y;
};

template<typename T> int f(T p) requires HasMult<T> {
    std::cout << "TU2\n";
}

template int f(int);

void g() {
    f(2);
}
```

## Bibliography

This bibliography lists the resources that were mentioned, adopted, or cited in this book. These days, many of the advancements in programming happen in electronic forums. It is therefore not surprising to find, in addition to the more traditional books and articles, quite a few Web sites. We do not claim that our list is close to being comprehensive. However, we do find that the resources are relevant contributions to the topic of C++ templates.

Web sites are typically considerably more volatile than books and articles. The Internet links listed here may not be valid in the future. Therefore, we provide the actual list of links for this book at the following site (and we expect this site to be stable): http://www.tmplbook.com

Before listing the books, articles, and Web sites, we introduce the more interactive kind of resources that are provided by *newsgroups*.

### Forums

In the first edition of this book, we referred to Usenet groups (a large collection of pre-world-wide-web on-line forums) as a source for discussions about the C++ programming language. Those groups have mostly faded since then but many other online programming communities have arisen, and several of these cater to C++ programmers. We list some of the most popular here:

- *Cppreference* is a “wiki” (i.e., collectively editable) of reference information about C and C++ (in various languages).
  - http://www.cppreference.com
- *Stack Overflow* is a broad developer community that also covers C++ and C++ templates in particular.
  - https://stackoverflow.com/questions/tagged/c%2b%2b
  - https://stackoverflow.com/questions/tagged/c%2b%2b%20templates
- *Quora* is similar to Stack Overflow, but not limited to technical discussions.
  - https://www.quora.com/topic/C++-programming-language
