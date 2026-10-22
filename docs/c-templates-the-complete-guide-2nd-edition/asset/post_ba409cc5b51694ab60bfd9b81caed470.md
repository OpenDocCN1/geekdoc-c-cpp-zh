
```
PushFront<int, Typelist<long>>
```

```
PushFront<short, Typelist<int, long>>
```

typelist/typelistreverse.hpp

```
template<typename List, bool Empty = IsEmpty<List>::value>
class ReverseT;

template<typename List>
using Reverse = typename ReverseT<List>::Type;

// recursive case:
template<typename List>
class ReverseT<List, false>
  : public PushBackT<Reverse<PopFront<List>>, Front<List>> { };

// basis case:
template<typename List>
class ReverseT<List, true>
{
  public:
    using Type = List;
};
```

typelist/addconst.hpp

```
template<typename T>
struct AddConstT
{
    using Type = T const;
};

template<typename T>
using AddConst = typename AddConstT<T>::Type;
```

typelist/transform.hpp
template<typename List, template<typename T> class MetaFun,
    bool Empty = IsEmpty<List>::value>
class TransformT;

// recursive case:
template<typename List, template<typename T> class MetaFun>
class TransformT<List, MetaFun, false>
: public PushFrontT<typename TransformT<PopFront<List>, MetaFun>::Type,
    typename MetaFun<Front<List>>::Type>
{
};

// basis case:

```
template<typename List, template<typename T> class MetaFun>
class TransformT<List, MetaFun, true>
{
public:
    using Type = List;
};

template<typename List, template<typename T> class MetaFun>
using Transform = typename TransformT<List, MetaFun>::Type;
```

typelist/accumulate.hpp

template<typename List,
    template<typename X, typename Y> class F,
    typename I,
    bool = IsEmpty<List>::value>
class AccumulateT;

// recursive case:
template<typename List,
    template<typename X, typename Y> class F,
    typename I>
class AccumulateT<List, F, I, false>
  : public AccumulateT<PopFront<List>, F,
            typename F<I, Front<List>>::Type>
{};

// basis case:
template<typename List,
    template<typename X, typename Y> class F,
    typename I>
class AccumulateT<List, F, I, true>
{
public:
  using Type = I;
};

template<typename List,
    template<typename X, typename Y> class F,
    typename I>
using Accumulate = typename AccumulateT<List, F, I>::Type;

```
```cpp
using Result = Accumulate<SignedIntegralTypes, PushFrontT, Typelist<>>;
// produces TypeList<long long, long, int, short, signed char>
```
```

typelist/largesttypeacc0.hpp

template<typename T, typename U>
class LargerTypeT
  : public IfThenElseT<sizeof(T) >= sizeof(U), T, U>
{
};

template<typename Typelist>
class LargestTypeAccT
  : public AccumulateT<PopFront<Typelist>, LargerTypeT,
                        Front<Typelist>>
{
};

template<typename Typelist>
using LargestTypeAcc = typename LargestTypeAccT<Typelist>::Type;

```
```cpp
// typelist/largesttypeacc.hpp

template<typename T, typename U>
class LargerTypeT
  : public IfThenElseT<(sizeof(T) >= sizeof(U)), T, U>
{
};

template<typename Typelist, bool = IsEmpty<Typelist>::value>
class LargestTypeAccT;

template<typename Typelist>
class LargestTypeAccT<Typelist, false>
  : public AccumulateT<PopFront<Typelist>, LargerTypeT,
                       Front<Typelist>>
{
};

template<typename Typelist>
class LargestTypeAccT<Typelist, true>
{
};

template<typename Typelist>
using LargestTypeAcc = typename LargestTypeAccT<Typelist>::Type;
```

typelist/insertionsort.hpp

template<typename List,
    template<typename T, typename U> class Compare,
    bool = IsEmpty<List>::value>
class InsertionSortT;

template<typename List,
    template<typename T, typename U> class Compare>
using InsertionSort = typename InsertionSortT<List, Compare>::Type;

// recursive case (insert first element into sorted list):
template<typename List,
    template<typename T, typename U> class Compare>
class InsertionSortT<List, Compare, false>
: public InsertSortedT<InsertionSort<PopFront<List>, Compare>,
    Front<List>, Compare>
{
};

// basis case (an empty list is sorted):
template<typename List,
    template<typename T, typename U> class Compare>
class InsertionSortT<List, Compare, true>
{
public:
    using Type = List;
};

# typelist/insertsorted.hpp

```
#include "identity.hpp"

template<typename List, typename Element,
    template<typename T, typename U> class Compare,
    bool = IsEmpty<List>::value>
class InsertSortedT;

// recursive case:
template<typename List, typename Element,
    template<typename T, typename U> class Compare>
class InsertSortedT<List, Element, Compare, false>
{
    // compute the tail of the resulting list:
    using NewTail =
        typename IfThenElse<Compare<Element, Front<List>>::value,
            IdentityT<List>,
            InsertSortedT<PopFront<List>, Element, Compare>
        >::Type;
    // compute the head of the resulting list:
    using NewHead = IfThenElse<Compare<Element, Front<List>>::value,
            Element,
            Front<List>>;
public:
    using Type = PushFront<NewTail, NewHead>;
};
```

```
// basis case:
template<typename List, typename Element,
    template<typename T, typename U> class Compare>
class InsertSortedT<List, Element, Compare, true>
  : public PushFrontT<List, Element>
{};

template<typename List, typename Element,
    template<typename T, typename U> class Compare>
using InsertSorted = typename InsertSortedT<List, Element, Compare>::Type;
```

```
template<typename List, typename Element,
    template<typename T, typename U> class Compare>
class InsertSortedT<List, Element, Compare, false>
: public IfThenElseT<Compare<Element, Front<List>>::value,
    PushFront<List, Element>,
    PushFront<InsertSorted<PopFront<List>,
        Element, Compare>,
        Front<List>>>
{
};
```

typelist/insertionsorttest.hpp

```
template<typename T, typename U>
struct SmallerThanT {
    static constexpr bool value = sizeof(T) < sizeof(U);
};

void testInsertionSort()
{
    using Types = Typelist<int, char, short, double>;
    using ST = InsertionSort<Types, SmallerThanT>;
    std::cout << std::is_same<ST,Typelist<char, short, int, double>>::value
              << '\n';
}
```

# typelist/ctvalue.hpp

```
```cpp
template<typename T, T Value>
struct CTValue
{
    static constexpr T value = Value;
};
```
```

```
using Primes = Typelist<CTValue<int, 2>, CTValue<int, 3>,
    CTValue<int, 5>, CTValue<int, 7>,
    CTValue<int, 11>>;
```

```
```cpp
// typelast/multiply.hpp

template<typename T, typename U>
struct MultiplyT;

template<typename T, T Value1, T Value2>
struct MultiplyT<CTValue<T, Value1>, CTValue<T, Value2>> {
public:
    using Type = CTValue<T, Value1 * Value2>;
};

template<typename T, typename U>
using Multiply = typename MultiplyT<T, U>::Type;
```
```

typelist/cttypelist.hpp

```
template<typename T, T... Values>
using CTTypelist = Typelist<CTValue<T, Values>...>; 
```

```
using Primes = CTTypelist<int, 2, 3, 5, 7, 11>;
```

typelist/valuelist.hpp

```
template<typename T, T... Values>
struct Valuelist {
};

template<typename T, T... Values>
struct IsEmpty<Valuelist<T, Values...>> {
    static constexpr bool value = sizeof...(Values) == 0;
};

template<typename T, T Head, T... Tail>
struct FrontT<Valuelist<T, Head, Tail...>> {
    using Type = CTValue<T, Head>;
    static constexpr T value = Head;
};

template<typename T, T Head, T... Tail>
struct PopFrontT<Valuelist<T, Head, Tail...>> {
    using Type = Valuelist<T, Tail...>;
};
```

```
```cpp
template<typename T, T... Values, T New>
struct PushFrontT<Valuelist<T, Values...>, CTValue<T, New>> {
  using Type = Valuelist<T, New, Values...>;
};

template<typename T, T... Values, T New>
struct PushBackT<Valuelist<T, Values...>, CTValue<T, New>> {
  using Type = Valuelist<T, Values..., New>;
};
```
```

typelist/valuelisttest.hpp

```
template<typename T, typename U>
struct GreaterThanT;

template<typename T, T First, T Second>
struct GreaterThanT<CTValue<T, First>, CTValue<T, Second>> {
    static constexpr bool value = First > Second;
};

void valuelisttest()
{
    using Integers = Valuelist<int, 6, 2, 4, 9, 5, 2, 1, 7>;

    using SortedIntegers = InsertionSort<Integers, GreaterThanT>;

    static_assert(std::is_same_v<SortedIntegers,
                Valuelist<int, 9, 7, 6, 5, 4, 2, 2, 1>>,
                "insertion sort failed");
}
```
