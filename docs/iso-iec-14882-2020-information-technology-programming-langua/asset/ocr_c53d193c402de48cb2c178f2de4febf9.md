```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
    class ForwardIterator, class Compare>
ForwardIterator
    set_symmetric_difference(ExecutionPolicy&& exec,
                            ForwardIterator1 first1, ForwardIterator1 last1,
                            ForwardIterator2 first2, ForwardIterator2 last2,
                            ForwardIterator result, Compare comp);
```

```
template<input_iterator I1, sentinel_for<I1> S1, input_iterator I2, sentinel_for<I2> S2,
    weakly_incrementable 0, class Comp = ranges::less,
    class Proj1 = identity, class Proj2 = identity>
requires mergeable<I1, I2, 0, Comp, Proj1, Proj2>
constexpr ranges::set_symmetric_difference_result<I1, I2, 0>
ranges::set_symmetric_difference(I1 first1, S1 last1, I2 first2, S2 last2, 0 result,
                                Comp comp = {}, Proj1 proj1 = {},
                                Proj2 proj2 = {});
```

```
template<input_range R1, input_range R2, weakly_incrementable 0,
    class Comp = ranges::less, class Proj1 = identity, class Proj2 = identity>
requires mergeable<iterator_t<R1>, iterator_t<R2>, 0, Comp, Proj1, Proj2>
constexpr ranges::set_symmetric_difference_result<borrowed_iterator_t<R1>, borrowed_iterator_t<R2>, 0>
ranges::set_symmetric_difference(R1&& r1, R2&& r2, 0 result, Comp comp = {},
                                Proj1 proj1 = {}, Proj2 proj2 = {});
```

1 Let comp be less{}, and proj1 and proj2 be identity{} for the overloads with no parameters by those names.

2 Preconditions: The ranges [first1, last1) and [first2, last2) are sorted with respect to comp and proj1 or proj2, respectively. The resulting range does not overlap with either of the original ranges.

3 Effects: Copies the elements of the range [first1, last1) that are not present in the range [first2, last2), and the elements of the range [first2, last2) that are not present in the range [first1, last1) to the range beginning at result. The elements in the constructed range are sorted.

4 Returns: Let result_last be the end of the constructed range. Returns

+   (4.1) — result_last for the overloads in namespace std.

+   (4.2) — {last1, last2, result_last} for the overloads in namespace ranges.

5 Complexity: At most 2 * ((last1 - first1) + (last2 - first2)) - 1 comparisons and applications of each projection.

6 Remarks: Stable (16.4.6.8). If [first1, last1) contains m elements that are equivalent to each other and [first2, last2) contains n elements that are equivalent to them, then |m − n| of those elements shall be copied to the output range: the last m − n of these elements from [first1, last1) if m > n, and the last n − m of these elements from [first2, last2) if m < n. In either case, the elements are copied in order.

# 25.8.8 Heap operations [alg.heap.operations]

# 25.8.8.1 General [alg.heap.operations.general]

1 A random access range [a, b) is a heap with respect to comp and proj for a comparator and projection comp and proj if its elements are organized such that:

+   (1.1) — With N = b - a, for all i, 0 < i < N, bool(invoke(comp, invoke(proj, a[⌊(i-1)/2⌋]), invoke(proj, a[i]))) is false.

+   (1.2) — *a may be removed by pop_heap, or a new element added by push_heap, in O(log N) time.

2 These properties make heaps useful as priority queues.

3 make_heap converts a range into a heap and sort_heap turns a heap into a sorted sequence.

# 25.8.8.2 push_heap [push.heap]

```
template<class RandomAccessIterator>
    constexpr void push_heap(RandomAccessIterator first, RandomAccessIterator last);
```