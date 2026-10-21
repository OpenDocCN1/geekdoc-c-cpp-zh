
## Deduction From Iterators

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

## std::array<> Deduction

A more interesting example is provided by class std::array<>. To be able to deduce both the element type and the number of elements:

```
std::array a{42, 45, 77};    // OK, deduces std::array<int,3>
```

the following deduction guide is defined (indirectly):

```
typename Allocator = allocator<pair<const Key, T>>
map(initializer_list<pair<const Key, T>>,
    Compare = Compare(),
    Allocator = Allocator())
-> map<Key, T, Compare, Allocator>;
}
```

All arguments are passed by value, therefore this deduction guide enabled the type of a passed comparator or allocator to decay as discussed. However, we naively used the same argument types, which meant that the initializer list took a const key type. As a consequence, the following did not work (as Ville Voutilainen pointed out in http://wg21.link/lwg3025):

```
std::pair elem1{1,2};
std::pair elem2{3,4};
...
std::map m1{elem1, elem2};    // ERROR with original C++17 guides
```

Because elem1 and elem2 are deduced as std::pair<int,int>, the deduction guide requiring a const type as first type in the pair did not match. Therefore, you still had to write the following:

```
std::map<int,int> m1{elem1, elem2};  // OK
```

As a consequence, in the deduction guide, the const had to be removed:

```
namespace std {
template<typename Key, typename T,
        typename Compare = less<Key>,
        typename Allocator = allocator<pair<const Key, T>>>
map(initializer_list<pair<Key, T>>,
    Compare = Compare(),
    Allocator = Allocator())
-> map<Key, T, Compare, Allocator>;
}
```

However, to still support the decay of the comparator and allocator, we also have to overload the deduction guide for a pair with const key type. Otherwise, the constructor would be used for class template argument deduction when passing a pair with a const key type, meaning that the deduction would differ slightly between passing pairs with const and non-const keys.

## No Deduction Guides for Smart Pointers

Note that some places in the C++ standard library do not have deduction guides even though you might expect them to be present.

You might expect to have deduction guides for shared and unique pointers, so that instead of:

```
std::shared_ptr<int> sp{new int(7)};
```

you could just write:

```
std::shared_ptr sp{new int(7)};      // not supported
```

This does not work automatically because the corresponding constructor is a template, which means that no implicit deduction guide applies:

```
namespace std {
    template<typename T> class shared_ptr {
        public:
            ...
            template<typename Y> explicit shared_ptr(Y* p);
            ...
    };
}
```

Y is a different template parameter to T, meaning that deducing Y from the constructor does not mean that we can deduce type T. This is a feature to be able to call something like:

```
std::shared_ptr<Base> sp{new Derived(...)};
```

The corresponding deduction guide would be simple to provide:

```
namespace std{
    template<typename Y> shared_ptr(Y*) -> shared_ptr<Y>;
}
```

However, this would also mean that this guide is taken when allocating arrays:

```
std::shared_ptr sp{new int[10]};      // OOPS: would deduce shared_ptr<int>
```

As so often in C++, we run into the nasty C problem that the type of a pointer to one object and an array of objects have or decay to the same type.

This problem seems dangerous and therefore, the C++ standards committee has decided not to support it.

For single objects, you still have to call:

```
std::shared_ptr<int> sp1{new int};      // OK
auto sp2 = std::make_shared<int>();      // OK
```

and for arrays:

```
std::shared_ptr<std::string> p(new std::string[10],
    [](std::string* p) {
        delete[] p;
    });
```

or, using the new feature to instantiate shared pointers for raw arrays, just:

```
std::shared_ptr<std::string[]> p{new std::string[10]};
```

## 9.3 Afternotes

Class template argument deduction was first proposed in 2007 by Michael Spertus in http://wg21.link/n2332. The proposal was revisited in 2013 by Michael Spertus and David Vandevoorde in http://wg21.link/n3602. The finally accepted wording was formulated by Michael Spertus, Faisal Vali, and Richard Smith in http://wg21.link/p0091r3, with modifications by Michael Spertus, Faisal Vali, and

Richard Smith in http://wg21.link/p0512r0, by Jason Merrill in http://wg21.link/p0620r0, and by Michael Spertus and Jason Merrill (as a defect report against C++17) in http://wg21.link/p702r1.

The support for class template argument deduction in the standard library was added by Michael Spertus, Walter E. Brown, and Stephan T. Lavavej in http://wg21.link/p0433r2 and (as a defect report against C++17) in http://wg21.link/p0739r0.

## Chapter 10

## Compile-Time if

With the syntax if constexpr(...), the compiler uses a compile-time expression to decide at compile time whether to use the then part or the else part (if any) of an if statement. The other part (if any) is discarded, meaning that no code is generated. This does not mean that the discarded part is completely ignored though. It will be checked just like the code of unused templates.

For example:

tmp l/ifcomptime.hpp

```
#include <string>

template<typename T>
std::string asString(T x)
{
    if constexpr(std::is_same_v<T, std::string>) {
        return x;        // statement invalid if no conversion to string
    }
    else if constexpr(std::is_arithmetic_v<T>) {
        return std::to_string(x); // statement invalid if x is not numeric
    }
    else {
        return std::string(x);    // statement invalid if no conversion to string
    }
}
```

By using if constexpr we decide at compile time whether we just return a passed string, call to_string() for a passed integral or floating-point value, or use a constructor to convert the passed argument to type std::string. The invalid calls are discarded, therefore the following code compiles (which would not be the case when using a regular runtime if):
