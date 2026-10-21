# Deduction From Iterators

To be able to deduce the type of the elements from iterators that define a range for initialization, containers have a deduction guide such as the following for std::vector<>:

```
// let std::vector<> deduce element type from initializing iterators:
namespace std {
    template<typename Iterator>
    vector(Iterator, Iterator)
        -> vector<typename iterator_traits<Iterator>::value_type>;
}
```

This allows, for example:

```
std::set<float> s;
std::vector v1(s.begin(), s.end());    // OK, deduces std::vector<float>
```

Note that the use of initialization with parentheses is important here. If you use curly braces:

```
std::vector v2{s.begin(), s.end()};    // BEWARE: doesn't deduce std::vector<float>
```

the two arguments are taken as elements of an initializer list (which has a higher priority according to the overload resolution rules). That is, it is equivalent to:

```
std::vector<std::set<float>::iterator> v2{s.begin(), s.end()};
```

meaning that we initialize a vector of two elements, the first referring to the first element and the second representing the position behind the last element.

On the other hand, consider:

```
std::vector v3{"hi", "world"};    // OK, deduces std::vector<const char*>
std::vector v4("hi", "world");    // OOPS: fatal runtime error
```

While the declaration of v3 also initializes the vector with two elements (both being string literals), the second causes a fatal runtime error, which hopefully causes a core dump. The problem is that string literals convert to character pointers, which are valid iterators. Thus, we pass two iterators that do not point to the same object. In other words: we pass an invalid range. We deduce a std::vector<const char>, but depending on the location of the two literals in memory, we get a bad_alloc exception, or we get a core dump because there is no distance at all, or we get a range of some undefined characters stored in between.

To summarize, using curly braces is always the best way to initialize the elements of a vector. The only exception is when a single vector is passed (where the copy constructor is preferred). When passing something else, it is better to use parentheses.

In any case, for a type with complicated constructors such as std::vector<> and other STL containers, it is highly recommended not to use class template argument deduction and instead, to specify the element type(s) explicitly.

# std::array<> Deduction

A more interesting example is provided by class std::array<>. To be able to deduce both the element type and the number of elements:

```
std::array a{42, 45, 77};    // OK, deduces std::array<int,3>
```

the following deduction guide is defined (indirectly):