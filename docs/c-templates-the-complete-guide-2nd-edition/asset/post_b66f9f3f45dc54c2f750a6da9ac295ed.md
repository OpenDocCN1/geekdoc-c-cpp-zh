
tuples/copycounter.hpp

```
template<int N>
struct CopyCounter
{
    inline static unsigned numCopies = 0;
    CopyCounter() {
    }
    CopyCounter(CopyCounter const&) {
        ++numCopies;
    }
};
```

tuples/copycountertest.hpp

```
void copycountertest()
{
    Tuple<CopyCounter<0>, CopyCounter<1>, CopyCounter<2>,
            CopyCounter<3>, CopyCounter<4>> copies;
    auto reversed = reverse(copies);
    std::cout << "0: " << CopyCounter<0>::numCopies << " copies\n";
    std::cout << "1: " << CopyCounter<1>::numCopies << " copies\n";
    std::cout << "2: " << CopyCounter<2>::numCopies << " copies\n";
    std::cout << "3: " << CopyCounter<3>::numCopies << " copies\n";
    std::cout << "4: " << CopyCounter<4>::numCopies << " copies\n";
}
```

```
auto reversed = makeTuple(get<4>(copies), get<3>(copies),
    get<2>(copies), get<1>(copies),
    get<0>(copies));
```

tuples/makeindexlist.hpp
// recursive case
template<unsigned N, typename Result = ValueList<unsigned>>
struct MakeIndexListT
  : MakeIndexListT<N-1, PushFront<Result, CTValue<unsigned, N-1>>>
{
};

// basis case
template<typename Result>
struct MakeIndexListT<0, Result>
{
    using Type = Result;
};

template<unsigned N>
using MakeIndexList = typename MakeIndexListT<N>::Type;

tuples/indexlistreverse.hpp

```
template<typename... Elements, unsigned... Indices>
auto reverseImpl(Tuple<Elements...> const& t,
                ValueList<unsigned, Indices...>)
{
    return makeTuple(get<Indices>(t)...);
}

template<typename... Elements>
auto reverse(Tuple<Elements...> const& t)
{
    return reverseImpl(t,
                    Reverse<MakeIndexList<sizeof...(Elements)>>());
}
```

```
-> decltype(makeTuple(get<Indices>(t)...))
```

tuples/select.hpp

```
template<typename... Elements, unsigned... Indices>
auto select(Tuple<Elements...> const& t,
    ValueList<unsigned, Indices...>)
{
    return makeTuple(get<Indices>(t)...);
}
```

```
Tuple<int, double, std::string> t1(42, 7.7, "hello}");
auto a = splat<1, 4>(t);
std::cout << a << '\n';
```

tuples/tuplesorttest.hpp

```
#include <complex>

template<typename T, typename U>
class SmallerThanT
{
public:
    static constexpr bool value = sizeof(T) < sizeof(U);
};

void testTupleSort()
{
    auto t1 = makeTuple(17LL, std::complex<double>(42,77), 'c', 42, 7.7);
    std::cout << t1 << '\n';
    auto t2 = sort<SmallerThanT>(t1); // t2 is Tuple<int, long, std::string>
    std::cout << "sorted by size: " << t2 << '\n';
}
```

```
```text
(17, (42,77), c, 42, 7.7)
sorted by size: (c, 42, 7.7, 17, (42,77))
```
```

tuples/tuplesort.hpp

// metafunction wrapper that compares the elements in a tuple:
template<typename List, template<typename T, typename U> class F>
class MetafunOfNthElementT {
public:
    template<typename T, typename U> class Apply;

    template<unsigned N, unsigned M>
    class Apply<CTValue<unsigned, M>, CTValue<unsigned, N>>
        : public F<NthElement<List, M>, NthElement<List, N>> { };
};

// sort a tuple based on comparing the element types:
template<template<typename T, typename U> class Compare,
         typename... Elements>
auto sort(Tuple<Elements...> const& t)
{
    return select(t,
                  InsertionSort<MakeIndexList<sizeof...(Elements)>,
                                MetafunOfNthElementT<
                                    Tuple<Elements...>, 
                                    Compare>::template Apply<>());
}
```

Tuple<std::string, char const*, int, char> t("Pi", "is roughly", 3, '\n');
apply(print, t); // OK: prints Pi is roughly 3

tuples/tuplestorage1.hpp

```
// recursive case:
template<typename Head, typename... Tail>
class Tuple<Head, Tail...> : private Tuple<Tail...>
{
    private:
        Head head;
    public:
        Head& getHead() { return head; }
        Head const& getHead() const { return head; }
        Tuple<Tail...>& getTail() { return *this; }
        Tuple<Tail...> const& getTail() const { return *this; }
};
```

tuples/tuplestorage2.hpp

```
template<typename... Types>
class Tuple;

template<typename T>
class TupleElt
{
    T value;

public:
    TupleElt() = default;

    template<typename U>
    TupleElt(U&& other) : value(std::forward<U>(other)) { }

    T& get() { return value; }
    T const& get() const { return value; }
};

// recursive case:
template<typename Head, typename... Tail>
class Tuple<Head, Tail...>
: private TupleElt<Head>, private Tuple<Tail...>
{
```

```
public:
    Head& getHead() {
        // potentially ambiguous
        return static_cast<TupleElt<Head> *>(this)->get();
    }
    Head const& getHead() const {
        // potentially ambiguous
        return static_cast<TupleElt<Head> const*>(this)->get();
    }
    Tuple<Tail...>& getTail() { return *this; }
    Tuple<Tail...> const& getTail() const { return *this; }
};

// basis case:
template<>
class Tuple<> {
    // no storage required
};
```

tuples/tupleelt1.hpp

```
template<unsigned Height, typename T>
class TupleElt {
    T value;
public:
    TupleElt() = default;

    template<typename U>
    TupleElt(U&& other) : value(std::forward<U>(other)) { }

    T&      get()      { return value; }
    T const& get() const { return value; }
};
```

tuples/tuplestorage3.hpp

```
template<typename... Types>
class Tuple;

// recursive case:
template<typename Head, typename... Tail>
class Tuple<Head, Tail...>
  : private TupleElt<sizeof...(Tail), Head>, private Tuple<Tail...>
{
  using HeadElt = TupleElt<sizeof...(Tail), Head>;
public:
  Head& getHead() {
    return static_cast<HeadElt *>(this)->get();
  }
  Head const& getHead() const {
    return static_cast<HeadElt const*>(this)->get();
  }
  Tuple<Tail...>& getTail() { return *this; }
  Tuple<Tail...> const& getTail() const { return *this; }
};

// basis case:
template<>
class Tuple<> {
  // no storage required
};
```

tuples/compressedtuple1.cpp

```
#include <algorithm>
#include "tupleelt1.hpp"
#include "tupelstorage3.hpp"
#include <iostream>

struct A {
    A() {
        std::cout << "A()" << '\n';
    }
};

struct B {
    B() {
        std::cout << "B()" << '\n';
    }
};

int main()
{
    Tuple<A, char, A, char, B> t1;
    std::cout << sizeof(t1) << " bytes" << '\n';
}
```

```
T&      get()      { return value; }
T const& get() const { return value; }
};

template<unsigned Height, typename T>
class TupleElt<Height, T, true> : private T
{
public:
    TupleElt() = default;
    template<typename U>
    TupleElt(U&& other) : T(std::forward<U>(other)) { }

    T&      get()      { return *this; }
    T const& get() const { return *this; }
};
```

tuples/constantget.hpp

```
template<unsigned H, typename T>
T& getHeight(TupleElt<H,T>& te)
{
    return te.get();
}

template<typename... Types>
class Tuple;

template<unsigned I, typename... Elements>
auto get(Tuple<Elements...>& t)
    -> decltype(getHeight<sizeof...(Elements)-I-1>(t))
{
    return getHeight<sizeof...(Elements)-I-1>(t);
}
```

```
template<typename T, T Index>
auto& operator[](CTValue<T, Index>) {
    return get<Index>(*this);
}
```

```
auto t = makeTuple(0, '1', 2.2f, std::string{"hello"});
auto a = t[CTValue<unsigned, 2>{}];
auto b = t[CTValue<unsigned, 3>{}];
```

# tuples/literals.hpp

```
#include "ctvalue.hpp"
#include <cassert>
#include <cstddef>

// convert single char to corresponding int value at compile time:
constexpr int toInt(char c) {
    // hexadecimal letters:
    if (c >= 'A' && c <= 'F') {
        return static_cast<int>(c) - static_cast<int>('A') + 10;
    }
    if (c >= 'a' && c <= 'f') {
        return static_cast<int>(c) - static_cast<int>('a') + 10;
    }
    // other (disable '.' for floating-point literals):
    assert(c >= '0' && c <= '9');
    return static_cast<int>(c) - static_cast<int>('0');
}
// parse array of chars to corresponding int value at compile time:
template<std::size_t N>
```
