
## 24.4 OPTIMIZING ALGORITHMS WITH PACK EXPANSIONS

Pack expansions (described in depth in Section 12.4.3 on page 201) can be a useful mechanism for offloading the work of typelist iteration to the compiler. The Transform() algorithm developed in Section 24.2.4 on page 589 is one that naturally lends itself to the use of a pack expansion, because it is applying the same operation to each of the elements in the list. This enables an algorithm specialization (by way of a partial specialization) for a Transform of a Typelist:

Click here to view code image

```cpp
template<typename... Elements, template<typename T> class MetaFun>
class Transform<Typelist<Elements...>, MetaFun>
{
public:
    using Type = Typelist<MetaFun<Elements>...>;
};
```

This implementation captures the typelist elements into a parameter pack `Elements`. It then employs a pack expansion with the pattern `MetaFun<Elements>...`. Typelist is then applied to the metafunction for each of the types in `Elements` and forms a typelist from the results. This implementation is arguably simpler, because it doesn't require recursion and uses language features in a fairly straightforward way. Moreover, it requires fewer template instantiations, because only one instance of the `Transform` template needs to be instantiated. The algorithm still requires a linear number of instantiations of `MetaFun`, but those instantiations are fundamental to the algorithm.

Other algorithms benefit similarly from use of pack expansions. For example, the Reverse algorithm described in Section 24.2.4 on page 557 requires a linear number of instantiations of `Reverse<T>`. With the pack expansion from Figure 24.??, the pack expansion requires only one instantiation of `Reverse` for each type in the typelist. Reverse is linear. However, the more-general recursive implementation of Reverse also delivers a linear number of instantiations.

Pack expansions can also be useful to select the elements in a given list of indices to produce a new typelist. The Select metaprogram takes in a typelist and a Valuelist containing indices into that typelist, then produces a new typelist containing the elements specified by the Valuelist:

Click here to view code image

```cpp
template<typename Types, typename Indices>
class Select;

template<typename Types, unsigned... Indices>
class Select<Types, Valuelist<unsigned, Indices...>>
{
public:
    using Type = Typelist<At<Types, Indices>...>;
};
```

This index list was captured in a parameter pack `Indices` and is expanded to produce a sequence of the `At` element types into the given typelist, capturing the result in a new Typelist. The following example illustrates how we can use Select to reverse a typelist:

Click here to view code image

```cpp
using SingleIntegerType =
    Typelist<int, char, short, int, long, long long>;
using ReversedSingleIntegerType =
    Select<SingleIntegerType, Valuelist<unsigned, 4, 3,
    2, 1, 0>>;
```

Prior to the introduction of variadic templates, typelists were generally formulated with a recursive data structure modeled after Lisp's cons cell. Each cons cell contains a value (the head of the list) and a nested list, the latter of which could either be another cons cell or the empty list, nil. This notion can be directly expressed in C++:

Click here to view code image

`typelist/cons.hpp`

```cpp
class Nil {};

template<typename HeadT, typename TailT = Nil>
class Cons {
public:
    using Head = HeadT;
    using Tail = TailT;
};
```

An empty typelist is written as Nil, while a single-element list containing it is written as Cons<int, Nil>, or more accurately, Cons<int, Nil>. Longer lists require nesting:

Click here to view code image

`typelist/cons.hpp`

```cpp
using TwoShort = Cons<short, Cons<short,
                         Cons<long,
                              Nil>>>;
```

Arbitrarily long typelists can be constructed by deep recursive nesting, although writing each long list by hand can become rather unwieldy:

Click here to view code image

```cpp
using SignedIntegralTypes = Cons<signed char, Cons<short,
                                      Cons<long, Cons<long long,
                                      Nil>>>>;
```

Extracting the first element in a cons-style list refers directly to the head of the list:

Click here to view code image

`typelist/consfront.hpp`

```cpp
template<typename List>
class Front {
public:
    using Type = typename List::Head;
};
```

Adding an element to the front wraps another Cons around the existing list:

Click here to view code image

`typelist/conspushfront.hpp`

```cpp
template<typename List, typename Element>
class PushFront {
public:
    using Type = Cons<Element, List>;
};
```

Finally, removing the first element from a recursive typelist extracts the tail of the list:

Click here to view code image

`typelist/conspopfront.hpp`

```cpp
template<typename List>
class PopFrontT {
public:
    using Type = typename List::Tail;
};

template<typename List>
using PopFront = typename PopFrontT<List>::Type;
```

An IsEmpty specialization for Nil completes the set of core typelist operations:

Click here to view code image

`typelist/consisempty.cpp`

```cpp
template<typename List>
struct IsEmpty {
    static constexpr bool value = false;
};

template<>
struct IsEmpty<Nil> {
    static constexpr bool value = true;
};
```

With these typelist operations, we can now use the InsertionSort algorithm defined in Section 24.3.2 on page 573, this time with cons-style lists.

Click here to view code image

`typelist/consInsert.cpp`

```cpp
template<typename T, typename U>
struct SmallerThan {
    static constexpr bool value = sizeof(T) < sizeof(U);
};

void consAssert()
{
    using ConsList = Cons<int, Cons<char, Cons<short, Cons<float>>>>;
    using SortedTypes = InsertionSort<ConsList, SmallerThan>;
    using Expected = Cons<char, Cons<short, Cons<int, Cons<float>>>>;

    std::cout << std::is_same<SortedTypes, Expected>::value;
}
```

As we've seen with the insertion sort, cons-style typelists can express all of the same algorithms as the variadic typelists described throughout this chapter. Indeed, many of the algorithms described are written in precisely the same style used to manipulate cons-style typelists. However, they have a few downsides that lead us to prefer the variadic versions. First, the nesting makes long cons-style typelists very hard to both write and, in source code and in compiler diagnostics. Second, several algorithms (including PushBack and Transform) can be specialized for variadic typelists to provide more efficient implementations (as measured by the number of instantiations). Finally, the use of variadic templates for typelists fits well with the use of variadic templates for heterogeneous containers, discussed in Chapter 2 and Chapter 25.

## 24.6 ALTERNATIVES

Typelists soon proved to have strong support shortly after the first C++ standard was published in 1998. Krzysztof Czarnecki and Ulrich Eisenecker introduced a LISP-inspired C++ style of integral constants in [Generative Programming], although they did not make the leap to general typelists.

Alexandrescu popularized this in his influential book, Modern C++ Design (Addison-Wesley Professional), above all, Alexandrescu demonstrated...

Abrahams and Gurtovoy provided much-needed structure for metaprogramming in [AbrahamsGurtovoy], describing abstractions for typelists, typelist algorithms, and related components in familiar terms drawn from the C++ standard library: sequences, iterators, algorithms, and metafunctions. The accompanying library, Boost.MPL ([BoostMPL]), is widely used for manipulating typelists.

- 1. There are even some platforms where bool is as large as long!
- 2. Note that the typelist could contain types to which sizeof does not apply, such as void. In this case, the compiler will produce an error, when attempting to compute the largest type of the typelist.
- 3. To experiment with this version of the algorithm, note that you will need to remove the partial specialization of typelist for typelist, or it will be used in lieu of the generic version.
- 4. Abrahams and Gurtovoy ([AbrahamsGurtovoy]) provide a much more in-depth discussion of compilation time for template metaprograms, including a number of techniques for reducing compile time. We only scratch the surface here.
- 5. Within the functional language community, this operation is typically known as map. However, we use the term transform to better align with the C++ standard library's algorithm names.
- 6. Within the functional language community, this operation is typically known as reduce. However, we use the term accumulate to better align with the C++ standard library's own algorithm names.
- 7. This also ensures that the result of accumulating an empty list will be the initial value.
- 8. The standard library defines the std::integral_constant template, which is a more featureful version of CTValue.
