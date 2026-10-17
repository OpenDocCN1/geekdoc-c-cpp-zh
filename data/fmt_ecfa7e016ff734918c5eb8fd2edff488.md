
# ISO/IEC 14882:2020(E)

```cpp
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class T>
void replace_copy_if(ExecutionPolicy& exec, // 25.5.3
    ForwardIterator1 first, ForwardIterator2 last,
    OutputIterator result,
    Predicate pred, const T& new_value);
```

```cpp
namespace ranges {
template<class I, class O>
    using copy_result = output_iterator<I, O>;

template<input_iterator I, sentinel_for<S> S, class T1, class T2, class Pro = identity>
output_iterator<I, Pro> = identity
requires indirectly_copyable<I, const T2& &&
    indirectly_binary_predicate<ranges::equal_to, projected<I, Pro>, T1*>
constexpr auto copy_result(I first, S last, const T1& old_value, const T2& new_value,
    Proj proj = {}) {};
}
```

# ISO/IEC 14882:2020(E)

```cpp
template<input_range R, class T1, class T2, output_iterator<const T2>&, O
class Proj = identity
requires indirectly_copyable<R, O> &&
    indirectly_binary_predicate<R, O> equal_to,
    projected_iterator<R, borrowed_iterator<R>, Proj, const T1*>
replace_copy(R&& r, R it, const T1& value, const T2& new_value,
    Proj proj) {};
template<class I, class O>
using result_iterator<I, sentinel_for<S>, class T, output_iterator<const T>
class Proj = identity, indirect_unary_predicate<projected<I, Proj>> Pred
requires indirectly_copyable<I, O>
replace_copy_if(I first, S last, Pred pred, const T& new_value,
    Proj proj) {};
template<input_range R, class T, output_iterator<const T> O, class Proj = identity,
    indirect_unary_predicate<projected<R, Proj>> Pred
requires indirectly_copyable<iterator_t<R>, O>
    projected_iterator<borrowed_iterator<R>, O>
replace_copy_if(R&& r, R it, Pred pred, const T& new_value,
    Proj proj) {};
}
```

```cpp
// 25.7.4
template<class T, class O>
class Forwarditerator {
    void fill(Forwarditerator first, Forwarditerator last, const T& value);
};
```

```cpp
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class Predicate>
ForwardIterator2
remove_if(ExecutionPolicy&& exec,                                   // 25.3.5
               ForwardIterator1 first, ForwardIterator1 last,
               ForwardIterator2 result, Predicate pred);
namespace ranges {
    template<class I, class O>
    using remove_copy_result = in_result<I, O>;
}
template<input_iterator I, sentinel_for<S> S, weakly_incremental<I>, class T,
           requires is_direct_iterator<I>
           indirect_binary_predicate<ranges::equal_to<I, Pro>, const T*>
           remove_copy_result<I, O> remove_copy(I first, S last, const T& value, Pro proj) = {};
template<input_range R, weakly_incremental<R>, class T, class Pro = identity>
           requires is_direct_iterator<R>
           indirect_binary_predicate_iterator_ranges<ranges::equal_to,
                                              projected_iterator<R, Pro>, const T*>
           remove_copy(R&& r, const T& value, Pro proj) = {};
template<class I, class O>
    using remove_copy_if = in_result<I, O>;
template<input_iterator I, sentinel_for<S> S, weakly_incremental<I>, indirect_unary_predicate<projected_iterator<I, Pro>> Pred>
           requires is_direct_iterator<I>
           remove_copy_result<I, O> remove_copy_if(I first, S last, Pred pred, Pro proj) = {};
template<input_range R, weakly_incremental<R>, projected_iterator<R, Pro>> Pred>
           requires is_direct_iterator(R)
           remove_copy_if(R&& r, Pred pred, Pro proj) = {};
// 25.3.9, unique
template<class ForwardIterator>
ForwardIterator unique(ForwardIterator first, ForwardIterator last);
template<class ForwardIterator, class BinaryPredicate>
ForwardIterator unique(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);
template<class ExecutionPolicy, class ForwardIterator>                                // 25.3.5
ForwardIterator unique(ExecutionPolicy&& exec,
                                                              ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class BinaryPredicate>                                // 25.3.5
ForwardIterator unique(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, BinaryPredicate pred);
namespace ranges {
    template<permutable I, sentinel_for<S> S, class Pro = identity>
    using indirect_equivalence_relation<projected_iterator<I, Pro>> ranges = ranges::equal_to;
    subrange<I> unique(I first, S last, const& comp, Pro proj) = {};
    template<forward_range R, class Pro = identity>
    indirect_equivalence_relation<projected_iterator<R, Pro>> ranges = ranges::equal_to;
    requires permutable<R>
    subrange<R> unique(R&& r, const& comp, Pro proj) = {};
}
```

# ISO/IEC 14882:2020(E)

```cpp
template<class InputIterator, class OutputIterator>
constexpr OutputIterator
unique_copy(InputIterator first, InputIterator last,
               OutputIterator result);

template<class InputIterator, class OutputIterator, class BinaryPredicate>
constexpr OutputIterator unique_copy(InputIterator first, InputIterator last,
               OutputIterator result, BinaryPredicate pred);

template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
ForwardIterator2
unique_copy(ExecutionPolicy&& exec,                                     // sec 25.3.5
               ForwardIterator1 first, ForwardIterator1 last,
               ForwardIterator2 result, BinaryPredicate pred);

namespace ranges {
    template<class I, class D>
    using copy_result = in_out_result<D>;

    template<input_iterator I, sentinel_for<S>, weakly_incrementable<O>, class Pro = identity,
           indirect_equivalence_relation<projected<I, Pro>> C = ranges::equal_to
           requires indirect_copyable<I, D>
           (forward_iterator<I> || (input_iterator<I> && std::same_as<typename iter_value_t<I>, D> &&
            indirect_copyable_storable<I, D>))
    copy_result
    unique_copy(I first, S last, O comp = {}, C c, Pro proj = {});

    template<input_range R, weakly_incrementable<O>, class Pro = identity,
           indirect_equivalence_relation<projected_iterator<R, Pro>> C = ranges::equal_to
           requires indirect_copyable<T, D>
           (forward_iterator<T> || (input_iterator<T> && std::same_as<typename iter_value_t<T>, iter_value_t<D>> &&
            indirect_copyable_storable<T, D>))
    copy_result
    unique_copy(R&& r, O comp = {}, C c, Pro proj = {});
}
```

```cpp
// 25.10, reverse
template<class BidirectionalIterator>
constexpr reverse(BidirectionalIterator first, BidirectionalIterator last);

template<class ExecutionPolicy, class BidirectionalIterator>
void reverse(ExecutionPolicy&& exec,                                     // sec 25.3.5
             BidirectionalIterator first, BidirectionalIterator last);

namespace ranges {
    template<bidirectional_iterator I, sentinel_for<S>
    requires permutable<I>
    constexpr reverse(I first, S last);

    template<backward_range R>
    requires permutable<R>
    constexpr reverse(R&& r);
}

template<class BidirectionalIterator, class OutputIterator>
constexpr OutputIterator
reverse(BidirectionalIterator first, BidirectionalIterator last);
```

```cpp
// 25.7.11, rotate
template<class ForwardIterator>
constexpr rotate(ForwardIterator first, ForwardIterator middle, ForwardIterator last);

template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator rotate(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator middle, ForwardIterator last);

namespace ranges {
    template<permutable I, sentinel_for<S>
    constexpr subrange<I> rotate(I first, I middle, S last);

    template<forward_range R>
    requires permutable<R>
    constexpr subrange<R> rotate(R&& r, iterator_t<R> middle);
}
```

```
// 25.7.12
```
