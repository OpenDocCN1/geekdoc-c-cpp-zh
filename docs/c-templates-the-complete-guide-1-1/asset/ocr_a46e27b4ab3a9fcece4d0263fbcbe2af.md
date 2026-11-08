# 24.4 OPTIMIZING ALGORITHMS WITH PACK EXPANSIONS

Pack expansions (described in depth in Section 12.4.3 on page 201) can be a useful mechanism for offloading the work of typelist iteration to the compiler. The Transform() algorithm developed in Section 24.2.4 on page 589 is one that naturally lends itself to the use of a pack expansion, because it is applying the same operation to each of the elements in the list. This enables an algorithm specialization (by way of a partial specialization) for a Transform of a Typelist:

Click here to view code image

```
template<typename... Elements, template<typename T> class MetaFun>
class Transform<Typelist<Elements...>, MetaFun<Elements>...>
{
public:
    using Type = Typelist<MetaFun<Elements>...>;
};
```

This implementation captures the typelist elements into a parameter pack `Elements`. It then employs a pack expansion with the pattern `MetaFun<Elements>...`. Typelist is then applied to the metafunction to each of the types in `Elements` and forms a typelist from the results. This implementation is arguably simpler, because it doesn't require recursion and uses language features in a fairly straightforward way. Moreover, it requires fewer template instantiations, because only one instance of the `Transform` template needs to be instantiated. The algorithm still requires a linear number of instantiations of `MetaFun`, but those instantiations are fundamental to the algorithm.

Other algorithms benefit similarly from use of pack expansions. For example, the Reverse algorithm described in Section 24.2.4 on page 557 requires a linear number of instantiations of `Reverse<T>`. With the pack expansion from Figure 24.??, the pack expansion requires only one instantiation of `Reverse` for each type in the typelist. Reverse is linear. However, the more-general recursive implementation of Reverse also delivers a linear number of instantiations.

Pack expansions can also be useful to select the elements in a given list of indices to produce a new typelist. The Select metaprogram takes in a typelist and a Valuelist containing indices into that typelist, then produces a new typelist containing the elements specified by the Valuelist:

Click here to view code image

```
template<typename Types, typename Indices>
class Select;

template<typename Types, unsigned... Indices>
class Select<Types, Valuelist<unsigned, Indices...>>
{
public:
    using Type = Typelist<At<Types, Indices>...>;
};
```

This indice was captured in a parameter pack `Types` and is expanded to produce a sequence of the `At` elements types into the given typelist, capturing the result in a new Typelist. The following example illustrates how we can use Select to reverse a typelist:

Click here to view code image

```
using SingleIntegerType =
    Typelist<int, char, short, int, long, long long>;
using ReversedSingleIntegerType =
    Select<SingleIntegerType, Valuelist<unsigned, 4, 3,
    2, 1, 0>>;
```