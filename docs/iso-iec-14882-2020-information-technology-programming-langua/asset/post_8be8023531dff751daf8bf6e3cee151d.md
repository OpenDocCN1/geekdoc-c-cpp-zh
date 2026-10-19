
```
template<input_range R1, input_range R2,
    class Pred = ranges::equal_to, class Proj1 = identity, class Proj2 = identity>
requires indirectly_comparable<iterator_t<R1>, iterator_t<R2>, Pred, Proj1, Proj2>
constexpr ranges::mismatch_result<borrowed_iterator_t<R1>, borrowed_iterator_t<R2>>
ranges::mismatch(R1&& r1, R2&& r2, Pred pred = {},
    Proj1 proj1 = {}, Proj2 proj2 = {});
```

1 Let last2 be first2 + (last1 - first1) for the overloads with no parameter last2 or r2.

2 Let E be:
- !( *(first1 + n) == *(first2 + n) ) for the overloads with no parameter pred;
- pred(*(first1 + n), *(first2 + n)) == false for the overloads with a parameter pred and no parameter proj1;
- !invoke(pred, invoke(proj1, *(first1 + n)), invoke(proj2, *(first2 + n))) for the overloads with both parameters pred and proj1.

3 Let N be min(last1 - first1, last2 - first2).

4 Returns: { first1 + n, first2 + n }, where n is the smallest integer in [0, N) such that E holds, or N if no such integer exists.

5 Complexity: At most N applications of the corresponding predicate and any projections.

## 25.6.11 Equal [alg.equal]

```
template<class InputIterator1, class InputIterator2>
constexpr bool equal(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
bool equal(ExecutionPolicy&& exec,
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2);
```

```
template<class InputIterator1, class InputIterator2,
    class BinaryPredicate>
constexpr bool equal(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, BinaryPredicate pred);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
    class BinaryPredicate>
bool equal(ExecutionPolicy&& exec,
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, BinaryPredicate pred);
```

```
template<class InputIterator1, class InputIterator2>
constexpr bool equal(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
bool equal(ExecutionPolicy&& exec,
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2);
```

```
template<class InputIterator1, class InputIterator2,
    class BinaryPredicate>
constexpr bool equal(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2,
    BinaryPredicate pred);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
    class BinaryPredicate>
bool equal(ExecutionPolicy&& exec,
    ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    BinaryPredicate pred);
```

```
template<input_iterator I1, sentinel_for<I1> S1, input_iterator I2, sentinel_for<I2> S2,
    class Pred = ranges::equal_to, class Proj1 = identity, class Proj2 = identity>
requires indirectly_comparable<I1, I2, Pred, Proj1, Proj2>
constexpr bool ranges::equal(I1 first1, S1 last1, I2 first2, S2 last2,
    Pred pred = {},
    Proj1 proj1 = {}, Proj2 proj2 = {});
template<input_range R1, input_range R2, class Pred = ranges::equal_to,
    class Proj1 = identity, class Proj2 = identity>
requires indirectly_comparable<iterator_t<R1>, iterator_t<R2>, Pred, Proj1, Proj2>
constexpr bool ranges::equal(R1&& r1, R2&& r2, Pred pred = {},
    Proj1 proj1 = {}, Proj2 proj2 = {});
```

Let:
- last2 be first2 + (last1 - first1) for the overloads with no parameter last2 or r2;
- pred be equal_to{} for the overloads with no parameter pred;
- E be:
  - pred(*i, *(first2 + (i - first1))) for the overloads with no parameter proj1;
  - invoke(pred, invoke(proj1, *i), invoke(proj2, *(first2 + (i - first1)))) for the overloads with parameter proj1.

Returns: If last1 - first1 != last2 - first2, return false. Otherwise return true if E holds for every iterator i in the range [first1, last) Otherwise, returns false.

Complexity: If the types of first1, last1, first2, and last2:
- meet the Cpp17RandomAccessIterator requirements (23.3.5.7) for the overloads in namespace std;
- pairwise model sized_sentinel_for (23.3.4.8) for the overloads in namespace ranges, and last1 - first1 != last2 - first2, then no applications of the corresponding predicate and each projection; otherwise,
- For the overloads with no ExecutionPolicy, at most min(last1 - first1, last2 - first2) applications of the corresponding predicate and any projections.
- For the overloads with an ExecutionPolicy, O(min(last1 - first1, last2 - first2)) applications of the corresponding predicate.

## 25.6.12 Is permutation [alg.is.permutation]

```
template<class ForwardIterator1, class ForwardIterator2>
constexpr bool is_permutation(ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2);
template<class ForwardIterator1, class ForwardIterator2,
    class BinaryPredicate>
constexpr bool is_permutation(ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, BinaryPredicate pred);
template<class ForwardIterator1, class ForwardIterator2>
constexpr bool is_permutation(ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2);
template<class ForwardIterator1, class ForwardIterator2,
    class BinaryPredicate>
constexpr bool is_permutation(ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    BinaryPredicate pred);
```

Mandates: ForwardIterator1 and ForwardIterator2 have the same value type.

Preconditions: The comparison function is an equivalence relation.

Remarks: If last2 was not given in the argument list, it denotes first2 + (last1 - first1) below.

Returns: If last1 - first1 != last2 - first2, return false. Otherwise return true if there exists a permutation of the elements in the range [first2, first2 + (last1 - first1)), beginning with ForwardIterator2 begin, such that equal(first1, last1, begin) returns true or equal(first1, last1, begin, pred) returns true; otherwise, returns false.

```
template<class InputIterator, class Size, class OutputIterator>
constexpr OutputIterator copy_n(InputIterator first, Size n,
    OutputIterator result);
```

```
template<class ExecutionPolicy, class ForwardIterator1, class Size, class ForwardIterator2>
ForwardIterator2 copy_n(ExecutionPolicy&& exec,
    ForwardIterator1 first, Size n,
    ForwardIterator2 result);
```

```
template<input_iterator I, weakly_incrementable O>
requires indirectly_copyable<I, O>
constexpr ranges::copy_n_result<I, O>
ranges::copy_n(I first, iter_difference_t<I> n, O result);
```

Let N be max(0, n).

Mandates: The type Size is convertible to an integral type (7.3.9, 11.4.8).

Effects: For each non-negative integer i < N, performs *(result + i) = *(first + i).

Returns:
- result + N for the overloads in namespace std.
- {first + N, result + N} for the overload in namespace ranges.

Complexity: Exactly N assignments.

```
template<class InputIterator, class OutputIterator, class Predicate>
constexpr OutputIterator copy_if(InputIterator first, InputIterator last,
    OutputIterator result, Predicate pred);
```

```
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
    class Predicate>
ForwardIterator2 copy_if(ExecutionPolicy&& exec,
    ForwardIterator1 first, ForwardIterator1 last,
    ForwardIterator2 result, Predicate pred);
```

```
template<input_iterator I, sentinel_for<I> S, weakly_incrementable O, class Proj = identity,
    indirect_unary_predicate<projected<I, Proj>> Pred>
requires indirectly_copyable<I, O>
constexpr ranges::copy_if_result<I, O>
ranges::copy_if(I first, S last, O result, Pred pred, Proj proj = {});
```

```
template<input_range R, weakly_incrementable O, class Proj = identity,
    indirect_unary_predicate<projected<iterator_t<R>, Proj>> Pred>
requires indirectly_copyable<iterator_t<R>, O>
constexpr ranges::copy_if_result<borrowed_iterator_t<R>, O>
ranges::copy_if(R&& r, O result, Pred pred, Proj proj = {});
```

Let E be:
- bool(pred(*i)) for the overloads in namespace std;
- bool(invoke(pred, invoke(proj, *i))) for the overloads in namespace ranges, and N be the number of iterators i in the range [first, last) for which the condition E holds.

Preconditions: The ranges [first, last) and [result, result + (last - first)) do not overlap.

[Note 1: For the overload with an ExecutionPolicy, a performance cost is possible if iterator_traits<ForwardIterator1>::value_type is not Cpp17MoveConstructible (Table 28). — end note]

Effects: Copies all of the elements referred to by the iterator i in the range [first, last) for which E is true.

Returns:
- result + N for the overloads in namespace std.
- {last, result + N} for the overload in namespace ranges.

Complexity: Exactly last - first applications of the corresponding predicate and any projection.

Remarks: Stable (16.4.6.8).
