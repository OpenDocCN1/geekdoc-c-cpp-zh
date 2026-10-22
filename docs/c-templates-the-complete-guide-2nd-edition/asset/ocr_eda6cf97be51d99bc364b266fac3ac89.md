The recursive case, which is also the primary definition of the template, walks through the typelist. Because the partial specialization guarantees that N > 0, the recursive case removes the front element from the list and requests the (N − 1)st element from the remaining list. In our example, Click here to view code image

```
NthElementT<Typelist<short, int, long>, 2> inherits from
```

Click here to view code image

```
NthElementT<Typelist<int, long>, 1> which then inherits from
```

Click here to view code image

```
NthElementT<Typelist<long>, 0> Here, we hit the basis case, and inheritance from FrontT<Typelist<long>> provides the result via the nested type Type.
```

# 24.2.2 Finding the Best Match

Many typelist algorithms search for data within the typelist. For example, one may want to find the largest type within the typelist (e.g., to allocate enough storage for any of the types in the list). This too can be accomplished with a recursive template metaprogram: Click here to view code image

typelist/largesttype.hpp

```
template<typename List>
class LargestTypeT;

// recursive case:
template<typename List>
class LargestTypeT
{
private:
using First = Front<List>;
using Rest = typename LargestTypeT<PopFront<List>>::Type;
public:
using Type = IfThenElse<(sizeof(First) >= sizeof(Rest)), First, Rest>;
};

// basis case:
template<>
class LargestTypeT<Typelist<>>
{
public:
using Type = char;
};
```