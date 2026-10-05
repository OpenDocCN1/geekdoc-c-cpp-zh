# Display 19.20 Set Operations

These functions work for sets, maps, multisets, and multimaps (and other containers) but do not work for containers. For example, they do not work for vectors, or deques unless their contents are sorted. For these to work, the elements in the container must be stored in order. These also work for forward iterators, which means they work for bidirectional and random-access iterators. (In some cases, even for other kinds of iterators that we have not covered in any detail.)

```
template <class ForwardIterator1, class ForwardIterator2>
bool includes(ForwardIterator1 first1, ForwardIterator1 last1,
              ForwardIterator2 first2, ForwardIterator2 last2);
// Returns true if every element in the range [first2, last2) occurs
// in the range [first1, last1). Otherwise, returns false.
// Time complexity: linear in the size of [first1, last1) plus [first2, last2].
```

```
template <class ForwardIterator1, class ForwardIterator2, class ForwardIterator3>
void* union(ForwardIterator1 first1, ForwardIterator1 last1,
            ForwardIterator2 first2, ForwardIterator2 last2,
            ForwardIterator3 result);
// Creates a sorted union of the ranges [first1, last1) and [first2, last2). The union is stored starting at result.
// Time complexity: linear in the size of [first1, last1) plus [first2, last2).
```

```
template <class ForwardIterator1, class ForwardIterator2>
void* set_intersection(ForwardIterator1 first1, ForwardIterator1 last1,
            ForwardIterator2 first2, ForwardIterator2 last2,
            ForwardIterator3 result);
// Creates a sorted intersection of the two ranges [first1, last1) and [first2, last2]. The intersection is stored starting at result.
// Time complexity: linear in the size of [first1, last1) plus [first2, last2).
```

```
template <class ForwardIterator1, class ForwardIterator2>
void* set_difference(ForwardIterator1 first1, ForwardIterator1 last1,
            ForwardIterator2 first2, ForwardIterator2 last2,
            ForwardIterator3 result);
// Creates a sorted set difference of the two ranges [first1, last1) and [first2, last2]. The difference consists of the elements in the first range that are not in the second. The result is stored starting at result.
// Time complexity: linear in the size of [first1, last1) plus [first2, last2).
```

> Returns an iterator of type ForwardIterator3 but can be used as a void function.