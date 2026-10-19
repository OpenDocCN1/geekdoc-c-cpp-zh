
## ISO/IEC 14882:2020(E)

```
template<random_access_iterator I, sentinel_for<I> S, class Comp = ranges::less, class Proj = identity>
  requires sortable<I, Comp, Proj>
  constexpr I
  ranges::make_heap(I first, S last, Comp comp = {}, Proj proj = {});
template<random_access_range R, class Comp = ranges::less, class Proj = identity>
  requires sortable<iterator_t<R>, Comp, Proj>
  constexpr borrowed_iterator_t<R>
  ranges::make_heap(R&& r, Comp comp = {}, Proj proj = {});
```

Let comp be less{} and proj be identity{} for the overloads with no parameters by those names.

Preconditions: For the overloads in namespace std, the type of *first meets the Cpp17MoveConstructible (Table 28) and Cpp17MoveAssignable (Table 30) requirements.

Effects: Constructs a heap with respect to comp and proj out of the range [first, last).

Returns: last for the overloads in namespace ranges.

Complexity: At most 3(last - first) comparisons and twice as many projections.

## 25.8.8.5 sort_heap [sort.heap]

```
template<class RandomAccessIterator>
  constexpr void sort_heap(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
  constexpr void sort_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);

template<random_access_iterator I, sentinel_for<I> S, class Comp = ranges::less, class Proj = identity>
  requires sortable<I, Comp, Proj>
  constexpr I
  ranges::sort_heap(I first, S last, Comp comp = {}, Proj proj = {});
template<random_access_range R, class Comp = ranges::less, class Proj = identity>
  requires sortable<iterator_t<R>, Comp, Proj>
  constexpr borrowed_iterator_t<R>
  ranges::sort_heap(R&& r, Comp comp = {}, Proj proj = {});
```

Let comp be less{} and proj be identity{} for the overloads with no parameters by those names.

Preconditions: The range [first, last) is a valid heap with respect to comp and proj. For the overloads in namespace std, RandomAccessIterator meets the Cpp17ValueSwappable requirements (16.4.4.3) and the type of *first meets the Cpp17MoveConstructible (Table 28) and Cpp17MoveAssignable (Table 30) requirements.

Effects: Sorts elements in the heap [first, last) with respect to comp and proj.

Returns: last for the overloads in namespace ranges.

Complexity: At most 2N log N comparisons, where N = last - first, and twice as many projections.

## 25.8.8.6 is_heap [is.heap]

```
template<class RandomAccessIterator>
  constexpr bool is_heap(RandomAccessIterator first, RandomAccessIterator last);
```

Effects: Equivalent to: return is_heap_until(first, last) == last;

```
template<class ExecutionPolicy, class RandomAccessIterator>
  bool is_heap(ExecutionPolicy&& exec,
               RandomAccessIterator first, RandomAccessIterator last);
```

Effects: Equivalent to:
  return is_heap_until(std::forward<ExecutionPolicy>(exec), first, last) == last;

## ISO/IEC 14882:2020(E)

```
template<forward_iterator I, sentinel_for<I> S, class Proj = identity,
    indirect_strict_weak_order<projected<I, Proj>> Comp = ranges::less>
constexpr I ranges::min_element(I first, S last, Comp comp = {}, Proj proj = {});
template<forward_range R, class Proj = identity,
    indirect_strict_weak_order<projected<iterator_t<R>, Proj>> Comp = ranges::less>
constexpr borrowed_iterator_t<R>
ranges::min_element(R&& r, Comp comp = {}, Proj proj = {});
```

Let comp be less{} and proj be identity{} for the overloads with no parameters by those names.

Returns: The first iterator i in the range [first, last) such that for every iterator j in the range [first, last),

    bool(invoke(comp, invoke(proj, *j), invoke(proj, *i)))

is false. Returns last if first == last.

Complexity: Exactly max(last - first - 1,0) comparisons and twice as many projections.

```
template<class ForwardIterator>
constexpr ForwardIterator max_element(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator max_element(ExecutionPolicy&& exec,
                            ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
constexpr ForwardIterator max_element(ForwardIterator first, ForwardIterator last,
                                      Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class Compare>
ForwardIterator max_element(ExecutionPolicy&& exec,
                            ForwardIterator first, ForwardIterator last,
                            Compare comp);
```

```
template<forward_iterator I, sentinel_for<I> S, class Proj = identity,
    indirect_strict_weak_order<projected<I, Proj>> Comp = ranges::less>
constexpr I ranges::max_element(I first, S last, Comp comp = {}, Proj proj = {});
template<forward_range R, class Proj = identity,
    indirect_strict_weak_order<projected<iterator_t<R>, Proj>> Comp = ranges::less>
constexpr borrowed_iterator_t<R>
ranges::max_element(R&& r, Comp comp = {}, Proj proj = {});
```

Let comp be less{} and proj be identity{} for the overloads with no parameters by those names.

Returns: The first iterator i in the range [first, last) such that for every iterator j in the range [first, last),

    bool(invoke(comp, invoke(proj, *i), invoke(proj, *j)))

is false. Returns last if first == last.

Complexity: Exactly max(last - first - 1,0) comparisons and twice as many projections.

```
template<class ForwardIterator>
constexpr pair<ForwardIterator, ForwardIterator>
minmax_element(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
pair<ForwardIterator, ForwardIterator>
minmax_element(ExecutionPolicy&& exec,
               ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
constexpr pair<ForwardIterator, ForwardIterator>
minmax_element(ForwardIterator first, ForwardIterator last, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class Compare>
pair<ForwardIterator, ForwardIterator>
minmax_element(ExecutionPolicy&& exec,
               ForwardIterator first, ForwardIterator last,
               Compare comp);
```

```
template<forward_iterator I, sentinel_for<I> S, class Proj = identity,
    indirect_strict_weak_order<projected<I, Proj>> Comp = ranges::less>
constexpr ranges::minmax_result<I>
ranges::minmax_element(I first, S last, Comp comp = {}, Proj proj = {});
template<forward_range R, class Proj = identity,
    indirect_strict_weak_order<projected<iterator_t<R>, Proj>> Comp = ranges::less>
constexpr ranges::minmax_result<borrowed_iterator_t<R>>
ranges::minmax_element(R&& r, Comp comp = {}, Proj proj = {});
```

Returns: {first, first} if [first, last) is empty, otherwise {m, M}, where m is the first iterator in [first, last) such that no iterator in the range refers to a smaller element, and where M is the last iterator²⁴⁰ in [first, last) such that no iterator in the range refers to a larger element.

Complexity: Let N be last - first. At most max(⌊3/2(N - 1)⌋,0) comparisons and twice as many applications of the projection, if any.

## 25.8.10 Bounded value [alg.clamp]

```
template<class T>
    constexpr const T& clamp(const T& v, const T& lo, const T& hi);
template<class T, class Compare>
    constexpr const T& clamp(const T& v, const T& lo, const T& hi, Compare comp);
template<class T, class Proj = identity,
    indirect_strict_weak_order<projected<const T*, Proj>> Comp = ranges::less>
constexpr const T&
ranges::clamp(const T& v, const T& lo, const T& hi, Comp comp = {}, Proj proj = {});
```

Let comp be less{} for the overloads with no parameter comp, and let proj be identity{} for the overloads with no parameter proj.

Preconditions: bool(comp(proj(hi), proj(lo))) is false. For the first form, type T meets the Cpp17LessThanComparable requirements (Table 26).

Returns: lo if bool(comp(proj(v), proj(lo))) is true, hi if bool(comp(proj(hi), proj(v))) is true, otherwise v.

[Note 1: If NaN is avoided, T can be a floating-point type. — end note]

Complexity: At most two comparisons and three applications of the projection.

## 25.8.11 Lexicographical comparison [alg.lex.comparison]

```
template<class InputIterator1, class InputIterator2>
    constexpr bool
    lexicographical_compare(InputIterator1 first1, InputIterator1 last1,
                            InputIterator2 first2, InputIterator2 last2);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
    bool
    lexicographical_compare(ExecutionPolicy&& exec,
                            ForwardIterator1 first1, ForwardIterator1 last1,
                            ForwardIterator2 first2, ForwardIterator2 last2);
```

```
template<class InputIterator1, class InputIterator2, class Compare>
    constexpr bool
    lexicographical_compare(InputIterator1 first1, InputIterator1 last1,
                            InputIterator2 first2, InputIterator2 last2,
                            Compare comp);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
    class Compare>
    bool
    lexicographical_compare(ExecutionPolicy&& exec,
                            ForwardIterator1 first1, ForwardIterator1 last1,
                            ForwardIterator2 first2, ForwardIterator2 last2,
                            Compare comp);
```

240) This behavior intentionally differs from max_element.
