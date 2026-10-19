

Let proj be identity{} for the overloads with no parameter named proj and let E(x) be bool(invoke(pred, invoke(proj, x))).

Preconditions: For the overloads in namespace std, ForwardIterator meets the Cpp17ValueSwappable requirements (16.4.4.3).

Effects: Places all the elements e in [first, last) that satisfy E(e) before all the elements that do not.

Returns: Let i be an iterator such that E(*j) is true for every iterator j in [first, i) and false for every iterator j in [i, last). Returns:

- i for the overloads in namespace std.
- {i, last} for the overloads in namespace ranges.

Complexity: Let N = last - first:

- For the overload with no ExecutionPolicy, exactly N applications of the predicate and projection. At most N/2 swaps if the type of first meets the Cpp17BidirectionalIterator requirements for the overloads in namespace std or models bidirectional_iterator for the overloads in namespace ranges, and at most N swaps otherwise.
- For the overload with an ExecutionPolicy, O(N log N) swaps and O(N) applications of the predicate.

```
template<class BidirectionalIterator, class Predicate>
BidirectionalIterator
    stable_partition(BidirectionalIterator first, BidirectionalIterator last, Predicate pred);
template<class ExecutionPolicy, class BidirectionalIterator, class Predicate>
BidirectionalIterator
    stable_partition(ExecutionPolicy&& exec,
        BidirectionalIterator first, BidirectionalIterator last, Predicate pred);
```

```
template<bidirectional_iterator I, sentinel_for<I> S, class Proj = identity,
    indirect_unary_predicate<projected<I, Proj>> Pred>
requires permutable<I>
subrange<I> ranges::stable_partition(I first, S last, Pred pred, Proj proj = {});
template<bidirectional_range R, class Proj = identity,
    indirect_unary_predicate<projected<iterator_t<R>, Proj>> Pred>
requires permutable<iterator_t<R>>
borrowed_subrange_t<R> ranges::stable_partition(R&& r, Pred pred, Proj proj = {});
```

Let proj be identity{} for the overloads with no parameter named proj and let E(x) be bool(invoke(pred, invoke(proj, x))).

Preconditions: For the overloads in namespace std, BidirectionalIterator meets the Cpp17ValueSwappable requirements (16.4.4.3) and the type of *first meets the Cpp17MoveConstructible (Table 28) and Cpp17MoveAssignable (Table 30) requirements.

Effects: Places all the elements e in [first, last) that satisfy E(e) before all the elements that do not. The relative order of the elements in both groups is preserved.

Returns: Let i be an iterator such that for every iterator j in [first, i), E(*j) is true, and for every iterator j in the range [i, last), E(*j) is false. Returns:

- i for the overloads in namespace std.
- {i, last} for the overloads in namespace ranges.

Complexity: Let N = last - first:

- For the overloads with no ExecutionPolicy, at most N log N swaps, but only O(N) swaps if there is enough extra memory. Exactly N applications of the predicate and projection.
- For the overload with an ExecutionPolicy, O(N log N) swaps and O(N) applications of the predicate.

```
template<class InputIterator, class OutputIterator1, class OutputIterator2, class Predicate>
constexpr pair<OutputIterator1, OutputIterator2>
    partition_copy(InputIterator first, InputIterator last,
        OutputIterator1 out_true, OutputIterator2 out_false, Predicate pred);
```

- For the overloads with an ExecutionPolicy, O(N) comparisons.

Remarks: Stable (16.4.6.8).

```
template<class BidirectionalIterator>
    void inplace_merge(BidirectionalIterator first,
                    BidirectionalIterator middle,
                    BidirectionalIterator last);
template<class ExecutionPolicy, class BidirectionalIterator>
    void inplace_merge(ExecutionPolicy&& exec,
                    BidirectionalIterator first,
                    BidirectionalIterator middle,
                    BidirectionalIterator last);
```

```
template<class BidirectionalIterator, class Compare>
    void inplace_merge(BidirectionalIterator first,
                    BidirectionalIterator middle,
                    BidirectionalIterator last, Compare comp);
template<class ExecutionPolicy, class BidirectionalIterator, class Compare>
    void inplace_merge(ExecutionPolicy&& exec,
                    BidirectionalIterator first,
                    BidirectionalIterator middle,
                    BidirectionalIterator last, Compare comp);
```

```
template<bidirectional_iterator I, sentinel_for<I> S, class Comp = ranges::less,
    class Proj = identity>
requires sortable<I, Comp, Proj>
I ranges::inplace_merge(I first, I middle, S last, Comp comp = {}, Proj proj = {});
```

Let comp be less{} and proj be identity{} for the overloads with no parameters by those names.

Preconditions: [first, middle) and [middle, last) are valid ranges sorted with respect to comp and proj. For the overloads in namespace std, BidirectionalIterator meets the Cpp17ValueSwappable requirements (16.4.4.3) and the type of *first meets the Cpp17MoveConstructible (Table 28) and Cpp17MoveAssignable (Table 30) requirements.

Effects: Merges two sorted consecutive ranges [first, middle) and [middle, last), putting the result of the merge into the range [first, last). The resulting range is sorted with respect to comp and proj.

Returns: last for the overload in namespace ranges.

Complexity: Let N = last - first:

- For the overloads with no ExecutionPolicy, and if enough additional memory is available, exactly N - 1 comparisons.
- Otherwise, O(N log N) comparisons.

In either case, twice as many projections as comparisons.

Remarks: Stable (16.4.6.8).

```
template<bidirectional_range R, class Comp = ranges::less, class Proj = identity>
requires sortable<iterator_t<R>, Comp, Proj>
borrowed_iterator_t<R>
ranges::inplace_merge(R&& r, iterator_t<R> middle, Comp comp = {}, Proj proj = {});
```

Effects: Equivalent to:

```
return ranges::inplace_merge(ranges::begin(r), middle, ranges::end(r), comp, proj);
```

## 25.8.7 Set operations on sorted structures [alg.set.operations]

### 25.8.7.1 General [alg.set.operations.general]

Subclause 25.8.7 defines all the basic set operations on sorted structures. They also work with multisets (22.4.7) containing multiple copies of equivalent elements. The semantics of the set operations are generalized to multisets in a standard way by defining set_union to contain the maximum number of occurrences of every element, set_intersection to contain the minimum, and so on.

### 25.8.7.2 includes [includes]

```
template<class InputIterator1, class InputIterator2>
constexpr bool includes(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2);
```

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
bool includes(ExecutionPolicy&& exec,
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2);
```

```
template<class InputIterator1, class InputIterator2, class Compare>
constexpr bool includes(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2,
    Compare comp);
```

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class Compare>
bool includes(ExecutionPolicy&& exec,
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    Compare comp);
```

```
template<input_iterator I1, sentinel_for<I1> S1, input_iterator I2, sentinel_for<I2> S2,
    class Proj1 = identity, class Proj2 = identity,
    indirect_strict_weak_order<projected<I1, Proj1>, projected<I2, Proj2>> Comp = ranges::less>
constexpr bool ranges::includes(I1 first1, S1 last1, I2 first2, S2 last2, Comp comp = {},
    Proj1 proj1 = {}, Proj2 proj2 = {});
```

```
template<input_range R1, input_range R2, class Proj1 = identity,
    class Proj2 = identity,
    indirect_strict_weak_order<projected<iterator_t<R1>, Proj1>, projected<iterator_t<R2>, Proj2>> Comp = ranges::less>
constexpr bool ranges::includes(R1&& r1, R2&& r2, Comp comp = {},
    Proj1 proj1 = {}, Proj2 proj2 = {});
```

1 Let comp be less{}, proj1 be identity{}, and proj2 be identity{}, for the overloads with no parameters by those names.

2 Preconditions: The ranges [first1, last1) and [first2, last2) are sorted with respect to comp and proj1 or proj2, respectively.

3 Returns: true if and only if [first2, last2) is a subsequence of [first1, last1).
[Note 1: A sequence S is a subsequence of another sequence T if S can be obtained from T by removing some, all, or none of T's elements and keeping the remaining elements in the same order. — end note]

4 Complexity: At most 2 * ((last1 - first1) + (last2 - first2)) - 1 comparisons and applications of each projection.

### 25.8.7.3 set_union [set.union]

```
template<class InputIterator1, class InputIterator2, class OutputIterator>
constexpr OutputIterator
set_union(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2,
    OutputIterator result);
```

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
    class ForwardIterator>
ForwardIterator
set_union(ExecutionPolicy&& exec,
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    ForwardIterator result);
```

```
template<class InputIterator1, class InputIterator2, class OutputIterator, class Compare>
constexpr OutputIterator
set_union(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2,
    OutputIterator result, Compare comp);
```

