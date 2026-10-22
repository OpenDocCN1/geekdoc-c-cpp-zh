```
return makeTuple(get<Indices>(t)...);
}
```

```
template<typename... Elements>
auto reverse(Tuple<Elements...> const& t)
{
return reverseImpl(t,
Reverse<MakeIndexList<sizeof...(Elements)>>());
}
```

In C++11, the return types have to be declared as Click here to view code image
-> decltype(makeTuple(get<Indices>(t)...)) and

Click here to view code image
-> decltype(reverseImpl(t, Reverse<MakeIndexList<sizeof...(Elements)>>())) The reverseImpl() function template captures the indices from its Valuelist parameter into a parameter pack Indices. It then returns the result of calling makeTuple() with arguments formed by calling get() on the tuple with the set of captured indices.

The reverse() algorithm itself merely forms the appropriate index set, as discussed earlier, and provides that to the reverseImpl algorithm. The indices are manipulated as a template metaprogram and therefore produce no run-time code. The only run-time code is in reverseImpl, which uses makeTuple() to construct the resulting tuple in one step and therefore copies the tuple elements only a single time.

# 25.3.6 Shuffle and Select

The reverseImpl() function template used in the previous section to form the reversed tuple actually contains no code specific to the reverse() operation. Rather, it simply selects a particular set of indices from an existing tuple and uses them to form a new tuple. reverse() provides a reversed set of indices, but many algorithms can build on this core tuple select() algorithm.⁴

Click here to view code image

tuples/select.hpp

```
template<typename... Elements, unsigned... Indices>
auto select(Tuple<Elements...> const& t,
Valuelist<unsigned, Indices...>)
{
```