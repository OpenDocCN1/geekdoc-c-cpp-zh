
traits/isclass.hpp

```
#include <type_traits>

template<typename T, typename = std::void_t<>>
struct IsClassT : std::false_type {      // primary template: by default no class
};

template<typename T>
struct IsClassT<T, std::void_t<int T::*>>  // classes can have pointer-to-member
: std::true_type {
};
```

traits/isenum.hpp

```
template<typename T>
struct IsEnumT {
    static constexpr bool value = !IsFundaT<T>::value &&
        !IsPointerT<T>::value &&
        !IsReferenceT<T>::value &&
        !IsArrayT<T>::value &&
        !IsPointerToMemberT<T>::value &&
        !IsFunctionT<T>::value &&
        !IsClassT<T>::value;
};
```

```
template<typename T>
struct RParam {
    using Type = typename IfThenElseT<sizeof(T)<=2*sizeof(void*),
        T,
        T const&>::Type;
};
```

```
template<typename T>
struct RParam<Array<T>> {
    using Type = Array<T> const&;
};
```

traits/rparam.hpp

```
#ifndef RPARAM_HPP
#define RPARAM_HPP

#include "ifthenelse.hpp"
#include <type_traits>

template<typename T>
struct RParam {
    using Type
        = IfThenElse<(sizeof(T) <= 2*sizeof(void*)
                     && std::is_trivially_copy_constructible<T>::value
                     && std::is_trivially_move_constructible<T>::value),
                     T,
                     T const&>;
};

#endif // RPARAM_HPP
```

traits/rparamcls.hpp

```
#include "rparam.hpp"
#include <iostream>

class MyClass1 {
public:
    MyClass1 () {
    }
    MyClass1 (MyClass1 const&) {
        std::cout << "MyClass1 copy constructor called\n";
    }
};

class MyClass2 {
public:
    MyClass2 () {
    }
    MyClass2 (MyClass2 const&) {
        std::cout << "MyClass2 copy constructor called\n";
    }
}
```

```
};

// pass MyClass2 objects with RParam<> by value
template<>
class RParam<MyClass2> {
    public:
        using Type = MyClass2;
};
```

traits/rparam2.cpp

```
#include "rparam.hpp"
#include "rparamcls.hpp"

// function that allows parameter passing by value or by reference
template<typename T1, typename T2>
void foo_core (typename RParam<T1>::Type p1,
               typename RParam<T2>::Type p2)
{
    ...
}

// wrapper to avoid explicit template parameter passing
template<typename T1, typename T2>
void foo (T1 && p1, T2 && p2)
{
    foo_core<T1,T2>(std::forward<T1>(p1),std::forward<T2>(p2));
}

int main()
{
    MyClass1 mc1;
    MyClass2 mc2;
    foo(mc1,mc2);  // same as foo_core<MyClass1,MyClass2>(mc1,mc2)
}
```

```
template<typename T> void f(T*);
template<typename T> void f(Array<T>);
```

```
template<typename T>
void swap(T& x, T& y)
{
    T tmp(x);
    x = y;
    y = tmp;
}
```

```
template<typename T>
void swap(Array<T>& x, Array<T>& y)
{
    swap(x.ptr, y.ptr);
    swap(x.len, y.len);
}
```

```
template<typename InputIterator, typename Distance>
void advanceIter(InputIterator& x, Distance n)
{
    while (n > 0) { // linear time
        ++x;
        --n;
    }
}
```

```
template<typename RandomAccessIterator, typename Distance>
void advanceIter(RandomAccessIterator& x, Distance n) {
    x += n;    // constant time
}
```

```
template<typename Iterator, typename Distance>
void advanceIterImpl(Iterator& x, Distance n, std::input_iterator_tag)
{
    while (n > 0) { // linear time
        ++x;
        --n;
    }
}

template<typename Iterator, typename Distance>
void advanceIterImpl(Iterator& x, Distance n,
                    std::random_access_iterator_tag) {
    x += n;        // constant time
}
```

```
template<typename Iterator, typename Distance>
void advanceIter(Iterator& x, Distance n)
{
    advanceIterImpl(x, n,
        typename
        std::iterator_traits<Iterator>::iterator_category());
}
```

```
namespace std {
    struct input_iterator_tag {};
    struct output_iterator_tag {};
    struct forward_iterator_tag : public input_iterator_tag {};
    struct bidirectional_iterator_tag : public forward_iterator_tag {};
    struct random_access_iterator_tag : public bidirectional_iterator_tag {};
}
```

```
template<typename Iterator>
constexpr bool IsRandomAccessIterator =
    IsConvertible<
        typename std::iterator_traits<Iterator>::iterator_category,
        std::random_access_iterator_tag>;

template<typename Iterator, typename Distance>
EnableIf<IsRandomAccessIterator<Iterator>>
advanceIter(Iterator& x, Distance n) {
    x += n;  // constant time
}
```

typeoverload/enableif.hpp

```
template<bool, typename T = void>
struct EnableIfT {
};

template<typename T>
struct EnableIfT<true, T> {
    using Type = T;
};

template<bool Cond, typename T = void>
using EnableIf = typename EnableIfT<Cond, T>::Type;
```

```
template<typename Iterator, typename Distance>
EnableIf<!IsRandomAccessIterator<Iterator>>
advanceIter(Iterator& x, Distance n)
{
    while (n > 0) { // linear time
        ++x;
        --n;
    }
}
```

```
advanceIter(Iterator& x, Distance n) {
    if (n > 0) {
        for ( ; n > 0; ++x, --n) { // linear time
        }
    } else {
        for ( ; n < 0; --x, ++n) { // linear time
        }
    }
}

// implementation for all other iterators:
template<typename Iterator, typename Distance>
EnableIf<!IsBidirectionalIterator<Iterator>>
advanceIter(Iterator& x, Distance n) {
    if (n < 0) {
        throw "advanceIter(): invalid iterator category for negative n";
    }
    while (n > 0) { // linear time
        ++x;
        --n;
    }
}
```

```
```cpp
#include <iterator>
#include "enable_if.hpp"
#include "isconvertible.hpp"

template<typename Iterator>
  constexpr bool IsInputIterator =
    IsConvertible<
      typename std::iterator_traits<Iterator>::iterator_category,
      std::input_iterator_tag>;

template<typename T>
class Container {
 public:
  // construct from an input iterator sequence:
  template<typename Iterator,
           typename = EnableIf<IsInputIterator<Iterator>>>
  Container(Iterator first, Iterator last);

  // convert to a container so long as the value types are convertible:
  template<typename U, typename = EnableIf<IsConvertible<T, U>>>
  operator Container<U>() const;
};
```
```

```
// construct from an input iterator sequence:
template<typename Iterator,
    typename = EnableIf<IsInputIterator<Iterator> &&
                    !IsRandomAccessIterator<Iterator>>>
```

typeoverload/advance3.hpp

```
template<typename Iterator, typename Distance>
void advanceIter(Iterator& x, Distance n) {
    if constexpr(IsRandomAccessIterator<Iterator>) {
        // implementation for random access iterators:
        x += n;                     // constant time
    }
    else if constexpr(IsBidirectionalIterator<Iterator>) {
        // implementation for bidirectional iterators:
        if (n > 0) {
            for ( ; n > 0; ++x, --n) {  // linear time for positive n
            }
        } else {
            for ( ; n < 0; --x, ++n) {  // linear time for negative n
            }
        }
    }
}
```

```
else {
    // implementation for all other iterators that are at least input iterators:
    if (n < 0) {
        throw "advanceIter(): invalid iterator category for negative n";
    }
    while (n > 0) {            // linear time for positive n only
        ++x;
        --n;
    }
}
}
```

```
template<typename T>
void f(T p) {
    if constexpr (condition<T>::value) {
        // do something here...
    }
    else {
        // not a T for which f() makes sense:
        static_assert(condition<T>::value, "can't call f() for such a T");
    }
}
```

typeoverload/container4.hpp

```
template<typename T>
class Container {
public:
    // construct from an input iterator sequence:
    template<typename Iterator>
    requires IsInputIterator<Iterator>
    Container(Iterator first, Iterator last);

    // construct from a random access iterator sequence:
    template<typename Iterator>
    requires IsRandomAccessIterator<Iterator>
    Container(Iterator first, Iterator last);

    // convert to a container so long as the value types are convertible:
    template<typename U>
    requires IsConvertible<T, U>
    operator Container<U>() const;
};
```
