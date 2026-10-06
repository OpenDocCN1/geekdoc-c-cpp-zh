Returns: lo if v is less than, hi if i is less than v, otherwise v.

> [Note: NaN is avoided, T can be a floating-point type. -- end note]

Complexity: At most two comparisons.

# 28.7.10 Lexographical comparison [alg.lex.comparison]

```
template<class InputIterator, class InputIterator2>
bool
    lexicographical_compare(Iterator1 first1, Iterator1 last1,
                             Iterator2 first2, Iterator2 last2);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
bool
    lexicographical_compare(ExecutionPolicy,
                             ForwardIterator1 first1, ForwardIterator1 last1,
                             ForwardIterator2 first2, ForwardIterator2 last2);
template<class InputIterator, class Compare, class Compare>
bool
    lexicographical_compare(Iterator1 first1, Iterator1 last1,
                             Iterator2 first2, Iterator2 last2,
                             Compare comp);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class Compare>
bool
    lexicographical_compare(ExecutionPolicy,
                             ForwardIterator1 first1, ForwardIterator1 last1,
                             ForwardIterator2 first2, ForwardIterator2 last2,
                             Compare comp);
```

Returns: true if the sequence of elements defined by the range [first1, last1) is lexicographically less than the sequence of elements defined by the range [first2, last2) and false otherwise.

Complexity: If two sequences have the same number of elements and their corresponding elements (if any) are equivalent, then neither is lexicographically less than the other. If one sequence is a prefix of the other, then the shorter sequence is lexicographically less than the longer sequence. Otherwise, the lexicographical comparison of the sequences yields the same result as the comparison of the first corresponding pairs of elements that are not equal.

[Example: The following sample implementation satisfies these requirements:

```
for (; first1 != last1 && first2 != last2; ++first1, ++first2) {
    if (*first1 < *first2) return false;
    if (*first2 < *first1) return true;
}
return first1 == last1 && first2 == last2;
```

> [Note: An empty sequence is lexicographically less than any non-empty sequence, but not less than any sequence. -- end note]

# 28.7.11 Permutation generators [alg.permutation.generators]

```
template<class BidirectionalIterator>
bool next_permutation(BidirectionalIterator first,
                     BidirectionalIterator last);
```