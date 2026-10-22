of PopFront: Click here to view code image

```
using Type = PushFront<PopFront<SignedIntegralTypes>, bool>;
// equivalent to Typelist<bool, short, int, long, long long>
```

Going further, we can implement algorithms—searches, transformations, reversals—as template metafunctions operating on typelists.

# 24.2.1 Indexing

One of the most fundamental operations on a typelist is to extract a specific element from the list. Section 24.1 illustrated how to implement an operation that extracts the first element. Here, we generalize this operation to extract the Nth element. For example, to extract the type at index 2 of the given typelist we can write: Click here to view code image

```
using TL = NthElement<Typelist<short, int, long>, 2>; which makes TL an alias for long. The NthElement operation is implemented with a recursive metaprogram that walks through the typelist until it finds the requested element: Click here to view code image
```

typelist/nthelement.hpp

```
// recursive case:
template<typename List, unsigned N>
class NthElementT : public NthElementT<PopFront<List>, N-1>
{};

// basis case:
template<typename List>
class NthElementT<List, 0> : public FrontT<List>
{};

template<typename List, unsigned N>
using NthElement = typename NthElementT<List, N>::Type;
```

First, consider the basis case, covered by the partial specialization where N is 0. This specialization terminates our recursion by providing the element at the front of the list. It does so by inheriting publicly from FrontT<List>, which (indirectly) provides the Type type alias that is both the front of this list and, therefore, the result of the NthElement metafunction, using metafunction forwarding (discussed in Section 19.3.2 on page 404).