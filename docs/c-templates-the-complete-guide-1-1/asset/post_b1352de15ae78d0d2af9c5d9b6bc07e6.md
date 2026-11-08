
```cpp
template<typename... Elements, unsigned... Indices>
auto reverseImpl(Tuple<Elements...> const& t,
                 ValueList<unsigned, Indices...>)
{
    return makeTuple(get<Indices>(t)...);
}
```

```cpp
template<typename... Elements>
auto reverse(Tuple<Elements...> const& t)
{
    return reverseImpl(t,
                       Reverse<MakeIndexList<sizeof...(Elements)>>{});
}
```

In C++11, the return types have to be deduced as

```cpp
-> decltype(makeTuple(get<Indices>(t)...))
```

and

```cpp
-> decltype(reverseImpl(t, Reverse<MakeIndexList<sizeof...(Elements)>>{}))
```

The reverseImpl() function template captures the indices from its ValueList parameter into a parameter pack Indices. It then returns the result of calling makeTuple() with arguments formed by calling get<> on the tuple with that pack of captured indices.

The reverse() algorithm itself merely forms the appropriate index set, as discussed earlier, and provides that to the reverseImpl() algorithm. This makes reverse() a redundant step and therefore produces no run-time code. The only run-time code is in reverseImpl, which uses no tuple<...> construct: the resulting tuple is formed in one step and therefore makes the tuple equally efficient at run time.

### 25.3.6 Shuffle and Select

The reverseImpl() function template used in the previous section to form the reversed tuple actually contains no code specific to the reverse() operation. Rather, it simply selects a particular set of indices from an existing tuple and uses them to form a new tuple. reverse() provides a reversed set of indices, but many algorithms can build on this more tuple select() algorithm:

tuple.hpp/select.hpp

```cpp
template<typename... Elements, unsigned... Indices>
auto select(Tuple<Elements...> const& t,
            ValueList<unsigned, Indices...>)
{
    return makeTuple(get<Indices>(t)...);
}
```

One simple algorithm that builds on select() is a simple "split" operation, which takes a single element in a tuple and replicates it to create another tuple with some number of copies of that element. For example:

```cpp
template<unsigned T, unsigned I, unsigned... Indices>
class ReplicatedIndexList<T, I, ValueList<unsigned, Indices...>>
{
public:
  ReplicatedIndexList<T, I>
    : ValueList<unsigned, Indices...>
  {
  }
};

template<unsigned T, unsigned... Indices>
class ReplicatedIndexList<T, 0, ValueList<unsigned, Indices...>>
{
public:
  using Type = ValueList<unsigned, Indices...>;
};

template<unsigned... I, unsigned... Indices>
using ReplicatedIndexList = typename ReplicatedIndexList<...>::Type;

template<unsigned... I, typename... Elements>
auto split(Tuple<Elements...> const& t)
{
  return select(t, ReplicatedIndexList<T, N>{});
}
```

Even compile-time tuple algorithms can also be implemented in terms of a metaprogram on the index list followed by an application of `select`. (For example, we can use the insertion sort developed in Section 2.4.3.7 on page 16 to sort a tuple based on the size of the element type. Given such a `sort` function, which accepts a template instantiation comparing tuple element types as the comparison operation, we could sort tuple elements by size with code like the following:

tuple2/tupleinsert.tpp

```cpp
#include <complex>

template<typename T, typename U>
class SmallerThan
{
public:
  static constexpr bool value = sizeof(T) < sizeof(U);
};

void testTupleSort()
{
  auto T1 = makeTuple(11.7, std::complex<double>(42, 7));
  std::cout << T1 << '\n';

  auto T2 = sortBySize<SmallerThan>(T1); // T2 is a Tuple...
  std::cout << "Sorted by size: " << T2 << '\n';
}
```

The output might, for example, be as follows:

```text
(17, (42,7), c, 42, 7)
Sorted by size: (c, 42, 7, 17, (42,7))
```

That might result in an implementation for tuple that is not quite the implementation with a tuple `select()`.

tuple2/tupleSort.tpp

```cpp
// metafunction wrapper that compares the elements in
class MetafunctionElement {
public:

  template<typename T, typename D = class Reply>

  template<typename U, unsigned N>
  class Apply<T, U, N> {
    using ...;
  };
};

// sort a tuple based on comparing the element types
template<typename T, typename D> class Compare {
  typename Element>

auto sort(Tuple<Elements...> const& t)
{
  return select(t,
    InsertionSort<MakeIndexList<...>>(
      MetafunctionElement<
        Tuple<Elements...>,
        Compare...>
    ));
}
```

Look carefully at the use of InsertionSort: The actual typelist to be sorted is a list of indices into the typelist, constructed with MakeIndexList<T>. Therefore, the result of the insertion sort is a set of indices into the tuple, which is then provided to select(). However, because the InsertionSort is operating on indices, it expects its comparison operation to compare two indices. The principal issue to understand when considering a sort of the indices of a data structure, as in the following (non-metaprogramming) example:

tuple2/insertsort.cpp

```cpp
#include <vector>
#include <algorithm>
#include <string>

int main()
{
  std::vector<std::string> strings = { "banana", "apple", "cherry" };
  std::vector<unsigned> indices = { 0, 1, 2 };

  std::sort(indices.begin(), indices.end(),
    [&strings](unsigned i, unsigned j) {
      return strings[i] < strings[j];
    });
}
```

Here, indices contains indices into the vector strings. The sort() operation sorts the actual indices, so the lambda provided as the comparison operation accepts two unsigned values (rather than their string values). However, the body of the lambda uses those unsigned values as indices into the strings vector, and the sorting is actually occurring in the context of the strings vector; at the end of the sort, indices provides indices into strings, sorted based on the values in strings.

Our use of InsertionSort for the tuple sort also employs the same approach. The Adapter template functor expects a template metafunction (its metaApply) that accepts two indices and then expands the indices into the corresponding elements from its tuple argument. In a sense, the member template Apply has "expanded" the typelist provided to its argument, in the same way that the lambda captured the strings vector from its enclosing scope. Apply performs the same function on the enclosing scope by passing the element types to the underlying Metafunction, completing the adaptation.

Notice that all of the computation for the sort is performed at compile time, and the resulting tuple is sorted directly, with no erroneous copying of values at run time.

value, regardless of what types or how many of those related values there are. At some point, it may be necessary to unpack such a tuple, for example, to pass its elements as separate arguments to a function. As a simple example, we may want to take a tuple and pass its elements to the variadic `printf()` operator described in Section 4.2.2 on page 100:

```text
Tuple-related: string, char const &, int, char * ("P1", "is roughly", 3, 7)

printf(t, ...); // ERROR: cannot expand a tuple; t is not a parameter pack
```

As noted in the example, the “obvious” attempt to unpack a tuple will not succeed, because it is not a parameter pack. We can achieve the same result using an index list. The following function template `apply()` accepts a function and a tuple, then calls the function with the unpacked tuple elements:

```cpp
template<typename F, typename... Elements, unsigned... Indices>
auto applyImpl(F f, Tuple<Elements...> const& t,
               ValueList<unsigned, Indices...>)
  -> decltype(f(get<Indices>(t)...))
{
  return applyImpl(f, t, MakeIndexList<sizeof...(Elements)>());
}

template<typename F, typename... Elements,
         unsigned N = sizeof...(Elements)>
auto apply(F f, Tuple<Elements...> const& t)
  -> decltype(applyImpl(f, t, MakeIndexList<N>()))
{
  return applyImpl(f, t, MakeIndexList<N>());
}
```

The `applyImpl()` function template takes a given index list and uses it to expand the elements of a tuple into the argument list for its function object argument. The user-facing `apply()` is responsible only for constructing the initial index list. Together, they allow us to expand a tuple into the arguments of `print()`:

```text
Tuple-related: string const &, int, char * ("P1", "is roughly", 3, 7)

apply(print, t); // OK: prints P1 is roughly 3
```

C++17 provides a similar function that works for any tuple-like type.

## 25.5 OPTIMIZING TUPLE

A tuple is a fundamental heterogeneous container with a large number of potential uses. As such, it is worthwhile to consider what can be done to optimize the tuple both in run time (storage, retention time) and at compile time (number of template instantiations). This section discusses a few specific optimizations to our Tuple implementation.

### 25.5.1 Tuples and the EBCO

Our current implementation for Tuple storage uses more storage than is strictly necessary. One problem is that the tail member will eventually be an empty tuple, because every nonempty tuple terminates with an empty tuple, and data members must always have at least one byte of storage.

To improve Tuple’s storage efficiency, we can apply the empty base class optimization (EBCO) discussed in Section 2.1 on page 49 by inheriting from the tuple rather than making it a member. For example:

```cpp
// recursive case

template<typename Head, typename... Tails>
class Tuple<Head, Tails...> : private Tuple<Tails...>
{
private:
  Head head;

public:
```
