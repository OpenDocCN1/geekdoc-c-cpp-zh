# 25.7.8 Remove [alg.remove]

```
template<class ForwardIterator, class T>
    constexpr ForwardIterator remove(ForwardIterator first, ForwardIterator last,
        const T& value);
template<class ExecutionPolicy, class ForwardIterator, class T>
    ForwardIterator remove(ExecutionPolicy&& exec,
        ForwardIterator first, ForwardIterator last,
        const T& value);
```

```
template<class ForwardIterator, class Predicate>
    constexpr ForwardIterator remove_if(ForwardIterator first, ForwardIterator last,
        Predicate pred);
template<class ExecutionPolicy, class ForwardIterator, class Predicate>
    ForwardIterator remove_if(ExecutionPolicy&& exec,
        ForwardIterator first, ForwardIterator last,
        Predicate pred);
```

```
template<permutable I, sentinel_for<I> S, class T, class Proj = identity>
    requires indirect_binary_predicate<ranges::equal_to, projected<I, Proj>, const T*>
    constexpr subrange<I> ranges::remove(I first, S last, const T& value, Proj proj = {});
template<forward_range R, class T, class Proj = identity>
    requires permutable<iterator_t<R>> &&
        indirect_binary_predicate<ranges::equal_to, projected<iterator_t<R>, Proj>, const T*>
    constexpr borrowed_subrange_t<R>
    ranges::remove(R&& r, const T& value, Proj proj = {});
```

```
template<permutable I, sentinel_for<I> S, class Proj = identity,
    indirect_unary_predicate<projected<I, Proj>> Pred>
    constexpr subrange<I> ranges::remove_if(I first, S last, Pred pred, Proj proj = {});
template<forward_range R, class Proj = identity,
    indirect_unary_predicate<projected<iterator_t<R>, Proj>> Pred>
    requires permutable<iterator_t<R>>
    constexpr borrowed_subrange_t<R>
    ranges::remove_if(R&& r, Pred pred, Proj proj = {});
```

Let E be

+   - bool(*i == value) for remove;
+   - bool(pred(*i)) for remove_if;
+   - bool(invoke(proj, *i) == value) for ranges::remove;
+   - bool(invoke(pred, invoke(proj, *i))) for ranges::remove_if.

Preconditions: For the algorithms in namespace std, the type of *first meets the Cpp17MoveAssignable requirements (Table 30).

Effects: Eliminates all the elements referred to by iterator i in the range [first, last) for which E holds.

Returns: Let j be the end of the resulting range. Returns:

+   - j for the overloads in namespace std.
+   - {j, last} for the overloads in namespace ranges.

Remarks: Stable (16.4.6.8).

Complexity: Exactly last - first applications of the corresponding predicate and any projection.

[Note 1: Each element in the range [ret, last), where ret is the returned value, has a valid but unspecified state, because the algorithms can eliminate elements by moving from elements that were originally in that range. — end note]

```
template<class InputIterator, class OutputIterator, class T>
    constexpr OutputIterator
    remove_copy(InputIterator first, InputIterator last,
        OutputIterator result, const T& value);
```