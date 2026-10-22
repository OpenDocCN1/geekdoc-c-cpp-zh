tuples/select.hpp

```
template<typename... Elements, unsigned... Indices>
auto select(Tuple<Elements...> const& t,
    ValueList<unsigned, Indices...>)
{
    return makeTuple(get<Indices>(t)...);
}
```