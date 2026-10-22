concept can express a predicate over multiple template parameters. For example:

Click here to view code image

```
template<typename T, typename U>
requires SomeConcept<T, U>
auto f(T x, U y) -> decltype(x+y) Thus, concepts can impose a
relationship between type parameters.
```

# Shorthand Notation for Single Requirements

To lighten the notational overhead of requires clauses, a syntactic shortcut is available when a constraint only involves one parameter at a time. This is perhaps most easily illustrated by using the shorthand for the declaration of our constrained max() template above: Click here to view code image

```
template<LessThanComparable T>
T max(T a, T b) {
return b < a ? a : b;
}
```

This is functionally equivalent to the prior definition of max(). When redeclaring a constrained template, however, the same form must be used as the original declaration (in that sense it is functionally equivalent, but not equivalent).

We can use the same shorthand for one of the two requirements in the find() template: Click here to view code image

```
template<Sequence Seq>
requires EqualityComparable<typename Seq::value_type>
typename Seq::iterator find(Seq const& seq,
typename Seq::value_type const& val)
{
return std::find(seq.begin(), seq.end(), val);
}
```

Again, this is equivalent to the prior definition of the find() template for sequence types.

# E.2 Defining Concepts

Concepts are much like constexpr variable templates of type bool, but the type is not explicitly specified: Click here to view code image

```
template<typename T> concept LessThanComparable = ... ; Here the "..." could perhaps be replaced by an expression that uses various traits
```