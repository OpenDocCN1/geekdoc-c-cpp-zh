
```cpp
template<mutable I, sentinel_for<I> S, class Pro = identity,
indirect_predicate<projected<I, Pro>> Pred>
constexpr partition(I first, S last, Predicate pred, Pro proj = {});
}
```

```cpp
template<forward_range, class Proj = identity,
indirect_unary_predicate<projected_iterator_t<R>, Proj> Pred>
requires mutable_iterator_t<R>
constexpr borrowed_subrange<R<R>
partition(R, r,, Proj =,```
```

```cpp
,, class,>
,icateicate
(BidirectionalIterator first,irectionalirectionalIterator first,
,);
template<class
Policy, class
irectionalIterator, class,,,, 25.3.5
BidirectionalIterator stable_partition(ExecutionPolicy&& exec,
BidirectionalIterator first,
Bidirectional
,
cpp
```

```cpp
ranges {
template<____,<_for<I>, =,, =
,
<_<<<,, Pro, Pro
subrange
_partition(I first, S last, Pred,,, proj);
template<bidirectional_range R, class Proj = identity,
indirect_predicate<projected_iterator_t<R>, Proj> Pred>
requires mutable_iterator_t<R>
borrowed_subrange_t<R> stable_partition(R&& r, Pred, Proj) = {};
}
```

```cpp
template<class Iterator1, class Iterator2, class Predicate>
constexpr pair<Iterator1, Iterator2>
partition_copy(Iterator1 first, Iterator2 last,
Iterator1& out_true, Iterator2& out_false,
Predicate);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
pair<ForwardIterator1, ForwardIterator2>
partition_copy(ExecutionPolicy&& exec, // sec 25.3.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator1& out_true, ForwardIterator2& out_false,
Predicate);
```

```cpp
namespace ranges {
template<class I, class O1, class O2>
using partition_copy_result = out_result<O1, O2>;
template<input_iterator I, sentinel_for<I> S,
weakly_incrementable<O1>, weakly_incrementable<O2>
class Proj = identity, indirect_unary_predicate<projected<I, Proj>> Pred>
requires indirectly_copyable<I, O1> && indirectly_copyable<I, O2>
constexpr partition_copy_result<O1, O2>
partition_copy(I first, S last, O1 out_true, O2 out_false, Pred,
Proj proj = {}) {
return {};
template<input_range R, weakly_incrementable O2,
class Proj = identity,
indirect_unary_predicate<projected_iterator_t<R>, Proj> Pred>
requires indirectly_copyable<iterator_t<R>, O1> &&
constexpr partition_copy_result<borrowed_subrange_t<R>, O2>
partition_copy(R&& r, O1 out_true, O2 out_false, Pred, Proj proj = {}) = {};
}
```

# ISO/IEC 14882:2020(E)

```cpp
template<class ForwardIterator, class Predicate>
constexpr ForwardIterator partition_point(ForwardIterator first, ForwardIterator last,
    Predicate pred);

namespace ranges {
template<forward_iterator I, sentinel_for<I> S, class Proj = identity,
indirect_predicate<projected_iterator<I>, Proj>>
constexpr I partition_point(I first, S last, Proj proj, Predicate pred = {});
template<forward_iterator R, class Proj = identity,
indirect_predicate<projected_iterator<R>, Proj>>
constexpr borrowed_iterator_t<R>
partition_point(R& r, Proj proj, Predicate pred = {});
}
```

## 25.5.6 merge

```cpp
template<class Iterator1, class Iterator2, class OutputIterator>
constexpr OutputIterator
merge(Iterator1 first1, Iterator1 last1,
    Iterator2 first2, Iterator2 last2,
    OutputIterator result);
template<class Iterator1, class Iterator2, class OutputIterator, class Compare>
constexpr OutputIterator
merge(Iterator1 first1, Iterator1 last1,
    Iterator2 first2, Iterator2 last2,
    OutputIterator result, Compare comp);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class Compare>
ForwardIterator2
merge(ExecutionPolicy&& exec, // 25.3.5
ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    OutputIterator result);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class Compare>
ForwardIterator2
merge(ExecutionPolicy&& exec, // 25.3.5
ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    OutputIterator result, Compare comp);

namespace ranges {
template<class I, class D>
using merge_result = in_out_result<I, D>;

template<input_iterator I1, sentinel_for<I1> S1, input_iterator I2, sentinel_for<I2> S2,
weakly_incrementable O, class Comp = ranges::less, class Proj1 = identity,
class Proj2 = identity>
requires mergeable<projected_iterator<I1, Proj1>, projected_iterator<I2, Proj2>, O, Comp, Proj1, Proj2>
constexpr merge_result<I1, O>
merge(I1 first1, S1 last1, I2 first2, S2 last2, O,
    Comp comp = {}, Proj1 proj1 = {}, Proj2 proj2 = {});

template<input_range R1, input_range R2, weakly_incrementable O, class Comp = ranges::less,
class Proj1 = identity, class Proj2 = identity>
requires mergeable<projected_iterator<R1, Proj1>, projected_iterator<R2, Proj2>, O, Comp, Proj1, Proj2>
constexpr merge_result<borrowed_iterator<R1>, O>
merge(R1&& r1, R1, R2&& r2, R2, O,
    Comp comp = {}, Proj1 proj1 = {}, Proj2 proj2 = {});
}
```

```cpp
# ISO/IEC 14882:2020(E)

template<class BidirectionalIterator>
void inplace_merge(BidirectionalIterator first,
    BidirectionalIterator middle,
    BidirectionalIterator last);

template<class BidirectionalIterator, class Compare>
void inplace_merge(BidirectionalIterator first,
    BidirectionalIterator middle,
    BidirectionalIterator last, Compare comp);

template<class ExecutionPolicy, class BidirectionalIterator>
void inplace_merge(ExecutionPolicy& exec, // 25.3.5
BidirectionalIterator first,
    BidirectionalIterator middle,
    BidirectionalIterator last);

template<class ExecutionPolicy, class BidirectionalIterator, class Compare>
void inplace_merge(ExecutionPolicy& exec, // 25.3.5
BidirectionalIterator first,
    BidirectionalIterator middle,
    BidirectionalIterator last, Compare comp);
```

```cpp
namespace ranges {
    template<bidirectional_iterator I, sentinel_for<I> S, class Comp = ranges::less,
    class Project = identity>
    requires comparable<I, Comp>
    inplace_merge(I first, I middle, S last, Comp comp = {}, Project proj = {});
    template<bidirectional_range R, class Comp = ranges::less, class Project = identity>
    requires sortable_iterator<R, Comp>
    borrowed_iterator_t<R>
    inplace_merge(R&& first, iterator_t<R> middle, Comp comp = {},
        Project proj = {});
}
```

```cpp
// 25.8.7, set operations
template<ExecutionPolicy, InputIterator1, InputIterator2>
constexpr bool includes(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2);
template<InputIterator1, InputIterator2, class Compare>
constexpr bool includes(InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2, Compare comp);
template<ExecutionPolicy, ForwardIterator1, ForwardIterator2, class ForwardIterator22> // 25.3.5
bool includes(ExecutionPolicy& exec, ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2);
template<ExecutionPolicy, ForwardIterator1, ForwardIterator2, class Compare>
bool includes(ExecutionPolicy& exec, ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2, Compare comp);

namespace ranges {
    template<I1, sentinel<I1> S1, I2, sentinel<I2> S2, Project1, Project2>
    requires mergeable<projected_iterator<I1, Project1>, projected_iterator<I2, Project2>>, Comp
    bool includes(I1 first1, S1 last1, I2 first2, S2 last2, Comp comp = {}, Project1 proj1 = {}, Project2 proj2 = {});
    template<input_range R1, input_range R2>
    requires mergeable<projected_iterator<R1, Project1>, projected_iterator<R2, Project2>>, Comp
    bool includes(R1&& r1, R1, R2&& r2, R2, Comp comp = {}, Project1 proj1 = {}, Project2 proj2 = {});
}
```

# ISO/IEC 14882:2020(E)

```cpp
template<class Iterator1, class InputIterator2, class OutputIterator>
constexpr OutputIterator
set_union(Iterator1 first1, Iterator1 last1,
    InputIterator2 first2, InputIterator2 last2,
    OutputIterator result);
template<class Iterator1, class InputIterator2, class OutputIterator, class Compare>
```
