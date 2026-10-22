StringLike, but not vice versa: Click here to view code image

```
int main()
{
printf(1); // selects template #1
printf("1"s); //selects template #2
}
```

We could imagine a string-like type that supports integer-like computations. For example, if "6"_NS and "7"_NS are two literals for that type, multiplying those literals would produce the same value as "42"_NS. Such a type might satisfy both IntegerLike and StringLike and, therefore, a call like print("42"_NS) would be ambiguous.

# E.3.1 Constraint Subsumption

Our first discussion of overloading function templates distinguished by constraints involved constraints that are expected to generally be mutually exclusive. For example, in our example with IntegerLike and StringLike, we could envision types that satisfy both concepts, but we expect that to be rare enough that our overloaded print templates remain useful.

There are, however, sets of concepts that are never mutually exclusive but where one “subsumes” the other. The classical examples of this are the standard library iterator categories: input iterator, forward iterator, bidirectional iterator, random access iterator, and, in C++17, contiguous iterator.¹ Suppose we have a definition for ForwardIterator: Click here to view code image

```
template<typename T>
concept ForwardIterator = ...; Then the “more refined” concept BidirectionalIterator might be defined as follows: Click here to view code image
```

```
template<typename T>
concept BidirectionIterator =
ForwardIterator<T> &&
requires (T it) {
{ --it } -> T&
};
```

That is, we add the ability to apply prefix operator-- on top of the capabilities already provided by forward iterators.

Consider now the std::advance() algorithm (which we’ll call