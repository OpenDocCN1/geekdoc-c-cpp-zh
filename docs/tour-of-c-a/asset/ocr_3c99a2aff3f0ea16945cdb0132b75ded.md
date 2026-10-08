# swappable<T,U> A T can be swapped with a U swappable_with<T,T>

Many algorithms work with combinations of related types, e.g., expressions with a mixture of ints doubles. We use common_with to say such a mix is mathematically sound. If common_with<X,Y> is true, we use common_type_t<X,Y> to compare a X with a Y by first converting to common_type_t<X,Y>. For example:

Click here to view code image

```
common_type<string, const char> s1 = some_fct()
common_type<string, const char> s2 = some_other_fct();
```

```
if (s1<s2) {
...
}
```

To specify a common type for a pair of types, we specialize common_type_t used in the definition of common. For example:

Click here to view code image

```
using common_type_t<Bigint,long> = Bigint; Il for a suitable definition of Bigint
```

Fortately, we don't need to define a common_type_t specialization unless we want to avoid operations on mixes of types for which a library doesn't (yet) have suitable definitions. The concepts related to comparison are strongly influenced by [Stepanov,2009].

| Comparison concepts <concepts> |
| --- | --- |
| equality_comparable_with<T,U> | A T and a U can be compared for equivalence using == equality_comparable<T> equality_comparable_with<T,T> |
| totally_ordered<T,U> | A T and a U can be compared using <, =, and >= yielding a total order |
| totally_ordered<T> | strict_totally_ordered_with<T,T> |
| three_way_comparable<T,U> | A T and a U can be compared using == yielding a consistent result |
| three_way_comparable<T> | three_way_comparable_with<T,T> |

The use of both equality_comparable_with and equality_comparable shows a (so far) missed opportunity to overload connections.

Curiously, there is no standard boolean concept. If I needed it, so here is a version:

```
template<typename B>
concept Boolean = requires(B x, B y) {
  {x = true};
  {x = false};
  {x = (x == y)};n  {x = (x != y)};n};
```