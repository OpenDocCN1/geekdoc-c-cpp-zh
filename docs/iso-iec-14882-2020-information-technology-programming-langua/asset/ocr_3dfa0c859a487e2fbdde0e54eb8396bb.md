(4.4) — comp induces a well-defined relation on the equivalence classes determined by equiv, and

(4.5) — the induced relation is a strict total ordering.

— end note]

5 A sequence is sorted with respect to a comp and proj for a comparator and projection comp and proj if for every iterator i pointing to the sequence and every non-negative integer n such that i + n is a valid iterator pointing to an element of the sequence,

bool(invoke(comp, invoke(proj, *(i + n)), invoke(proj, *i)))

is false.

6 A sequence [start, finish) is partitioned with respect to an expression f(e) if there exists an integer n such that for all 0 <= i < (finish - start), f(*(start + i)) is true if and only if i < n.

7 In the descriptions of the functions that deal with ordering relationships we frequently use a notion of equivalence to describe concepts such as stability. The equivalence to which we refer is not necessarily an operator==, but an equivalence relation induced by the strict weak ordering. That is, two elements a and b are considered equivalent if and only if !(a < b) && !(b < a).

# 25.8.2 Sorting [alg.sort]

# 25.8.2.1 sort [sort]

```
template<class RandomAccessIterator>
  constexpr void sort(RandomAccessIterator first, RandomAccessIterator last);
template<class ExecutionPolicy, class RandomAccessIterator>
  void sort(ExecutionPolicy&& exec,
            RandomAccessIterator first, RandomAccessIterator last);
```

```
template<class RandomAccessIterator, class Compare>
  constexpr void sort(RandomAccessIterator first, RandomAccessIterator last,
                      Compare comp);
template<class ExecutionPolicy, class RandomAccessIterator, class Compare>
  void sort(ExecutionPolicy&& exec,
            RandomAccessIterator first, RandomAccessIterator last,
            Compare comp);
```

```
template<random_access_iterator I, sentinel_for<I> S, class Comp = ranges::less,
         class Proj = identity>
  requires sortable<I, Comp, Proj>
  constexpr I
    ranges::sort(I first, S last, Comp comp = {}, Proj proj = {});
template<random_access_range R, class Comp = ranges::less, class Proj = identity>
  requires sortable<iterator_t<R>, Comp, Proj>
  constexpr borrowed_iterator_t<R>
    ranges::sort(R&& r, Comp comp = {}, Proj proj = {});
```

1 Let comp be less{} and proj be identity{} for the overloads with no parameters by those names.

2 Preconditions: For the overloads in namespace std, RandomAccessIterator meets the Cpp17ValueSwappable requirements (16.4.4.3) and the type of *first meets the Cpp17MoveConstructible (Table 28) and Cpp17MoveAssignable (Table 30) requirements.

3 Effects: Sorts the elements in the range [first, last) with respect to comp and proj.

4 Returns: last for the overloads in namespace ranges.

5 Complexity: Let N be last - first. O(N log N) comparisons and projections.

# 25.8.2.2 stable_sort [stable.sort]

```
template<class RandomAccessIterator>
  void stable_sort(RandomAccessIterator first, RandomAccessIterator last);
template<class ExecutionPolicy, class RandomAccessIterator>
  void stable_sort(ExecutionPolicy&& exec,
                   RandomAccessIterator first, RandomAccessIterator last);
```