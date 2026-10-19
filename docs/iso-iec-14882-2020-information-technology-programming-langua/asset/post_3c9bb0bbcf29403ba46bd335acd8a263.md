
## 25.11.4 uninitialized_value_construct [uninitialized.construct.value]

```
namespace ranges {
    template<no-throw-forward-range R>
        requires default_initializable<range_value_t<R>>
        borrowed_iterator_t<R> uninitialized_default_construct(R&& r);
}
```

Effects: Equivalent to:

```
for (; first != last; ++first)
    ::new (voidify(*first)) remove_reference_t<iter_reference_t<I>>;
    return first;
```

```
template<class NoThrowForwardIterator, class Size>
    NoThrowForwardIterator uninitialized_default_construct_n(NoThrowForwardIterator first, Size n);
```

Effects: Equivalent to:

```
for (; n > 0; (void)++first, --n)
    ::new (voidify(*first))
        typename iterator_traits<NoThrowForwardIterator>::value_type;
    return first;
```

```
namespace ranges {
    template<no-throw-forward-iterator I>
        requires default_initializable<iter_value_t<I>>
    I uninitialized_default_construct_n(I first, iter_difference_t<I> n);
}
```

Effects: Equivalent to:

```
return uninitialized_default_construct(counted_iterator(first, n),
    default_sentinel).base();
```

```
template<class NoThrowForwardIterator>
    void uninitialized_value_construct(NoThrowForwardIterator first, NoThrowForwardIterator last);
```

Effects: Equivalent to:

```
for (; first != last; ++first)
    ::new (voidify(*first))
        typename iterator_traits<NoThrowForwardIterator>::value_type();
```

```
namespace ranges {
    template<no-throw-forward-iterator I, no-throw-sentinel<I> S>
        requires default_initializable<iter_value_t<I>>
    I uninitialized_value_construct(I first, S last);
    template<no-throw-forward-range R>
        requires default_initializable<range_value_t<R>>
    borrowed_iterator_t<R> uninitialized_value_construct(R&& r);
}
```

Effects: Equivalent to:

```
for (; first != last; ++first)
    ::new (voidify(*first)) remove_reference_t<iter_reference_t<I>>();
    return first;
```

```
template<class NoThrowForwardIterator, class Size>
    NoThrowForwardIterator uninitialized_value_construct_n(NoThrowForwardIterator first, Size n);
```

Effects: Equivalent to:

```
for (; n > 0; (void)++first, --n)
    ::new (voidify(*first))
        typename iterator_traits<NoThrowForwardIterator>::value_type();
    return first;
```

```
namespace ranges {
    template<no-throw-forward-iterator I>
        requires default_initializable<iter_value_t<I>>
    I uninitialized_value_construct_n(I first, iter_difference_t<I> n);
}
```

## 25.11.5 uninitialized_copy [uninitialized.copy]

```
template<class InputIterator, class NoThrowForwardIterator>
NoThrowForwardIterator uninitialized_copy(InputIterator first, InputIterator last, NoThrowForwardIterator result);
```

Preconditions: result + [0, (last - first)) does not overlap with [first, last).

Effects: Equivalent to:

```
for (; first != last; ++result, (void) ++first)
::new (voidify(*result)) typename iterator_traits<NoThrowForwardIterator>::value_type(*first);
```

Returns: result.

```
namespace ranges {
template<input_iterator I, sentinel_for<I> S1, no-throw-forward-iterator O, no-throw-sentinel<O> S2>
requires constructible_from<iter_value_t<O>, iter_reference_t<I>>
uninitialized_copy_result<I, O>
uninitialized_copy(I ifirst, S1 ilast, O ofirst, S2 olast);
template<input_range IR, no-throw-forward-range OR>
requires constructible_from<range_value_t<OR>, range_reference_t<IR>>
uninitialized_copy_result<borrowed_iterator_t<IR>, borrowed_iterator_t<OR>>
uninitialized_copy(IR&& in_range, OR&& out_range);
}
```

Preconditions: [ofirst, olast) does not overlap with [ifirst, ilast).

Effects: Equivalent to:

```
for (; ifirst != ilast && ofirst != olast; ++ofirst, (void)++ifirst) {
::new (voidify(*ofirst)) remove_reference_t<iter_reference_t<O>>(*ifirst);
}
return {std::move(ifirst), ofirst};
```

```
template<class InputIterator, class Size, class NoThrowForwardIterator>
NoThrowForwardIterator uninitialized_copy_n(InputIterator first, Size n, NoThrowForwardIterator result);
```

Preconditions: result + [0, n) does not overlap with first + [0, n).

Effects: Equivalent to:

```
for (; n > 0; ++result, (void) ++first, --n) {
::new (voidify(*result)) typename iterator_traits<NoThrowForwardIterator>::value_type(*first);
}
```

Returns: result.

```
namespace ranges {
template<input_iterator I, no-throw-forward-iterator O, no-throw-sentinel<O> S>
requires constructible_from<iter_value_t<O>, iter_reference_t<I>>
uninitialized_copy_n_result<I, O>
uninitialized_copy_n(I ifirst, iter_difference_t<I> n, O ofirst, S olast);
}
```

Preconditions: [ofirst, olast) does not overlap with ifirst + [0, n).

Effects: Equivalent to:

```
auto t = uninitialized_copy(counted_iterator(ifirst, n), default_sentinel, ofirst, olast);
return {std::move(t.in).base(), t.out};
```

## 25.11.6 uninitialized_move [uninitialized.move]

```
template<class InputIterator, class NoThrowForwardIterator>
NoThrowForwardIterator uninitialized_move(InputIterator first, InputIterator last, NoThrowForwardIterator result);
```

Preconditions: result + [0, (last - first)) does not overlap with [first, last).

Effects: Equivalent to:

```
for (; first != last; (void)++result, ++first)
::new (voidify(*result))
typename iterator_traits<NoThrowForwardIterator>::value_type(std::move(*first));
return result;
```

```
namespace ranges {
template<input_iterator I, sentinel_for<I> S1,
no-throw-forward-iterator O, no-throw-sentinel<O> S2>
requires constructible_from<iter_value_t<O>, iter_rvalue_reference_t<I>>
uninitialized_move_result<I, O>
uninitialized_move(I ifirst, S1 ilast, O ofirst, S2 olast);
template<input_range IR, no-throw-forward-range OR>
requires constructible_from<range_value_t<OR>, range_rvalue_reference_t<IR>>
uninitialized_move_result<borrowed_iterator_t<IR>, borrowed_iterator_t<OR>>
uninitialized_move(IR&& in_range, OR&& out_range);
}
```

Preconditions: [ofirst, olast) does not overlap with [ifirst, ilast).

Effects: Equivalent to:

```
for (; ifirst != ilast && ofirst != olast; ++ofirst, (void)++ifirst) {
::new (voidify(*ofirst))
remove_reference_t<iter_reference_t<O>>(ranges::iter_move(ifirst));
}
return {std::move(ifirst), ofirst};
```

[Note 1: If an exception is thrown, some objects in the range [first, last) are left in a valid, but unspecified state. — end note]

```
template<class InputIterator, class Size, class NoThrowForwardIterator>
pair<InputIterator, NoThrowForwardIterator>
uninitialized_move_n(InputIterator first, Size n, NoThrowForwardIterator result);
```

Preconditions: result + [0, n) does not overlap with first + [0, n).

Effects: Equivalent to:

```
for (; n > 0; ++result, (void) ++first, --n)
::new (voidify(*result))
typename iterator_traits<NoThrowForwardIterator>::value_type(std::move(*first));
return {first, result};
```

```
namespace ranges {
template<input_iterator I, no-throw-forward-iterator O, no-throw-sentinel<O> S>
requires constructible_from<iter_value_t<O>, iter_rvalue_reference_t<I>>
uninitialized_move_n_result<I, O>
uninitialized_move_n(I ifirst, iter_difference_t<I> n, O ofirst, S olast);
}
```

Preconditions: [ofirst, olast) does not overlap with ifirst + [0, n).

Effects: Equivalent to:

```
auto t = uninitialized_move(counted_iterator(ifirst, n), default_sentinel, ofirst, olast);
return {std::move(t.in).base(), t.out};
```

[Note 2: If an exception is thrown, some objects in the range first + [0, n) are left in a valid but unspecified state. — end note]

## 25.11.7 uninitialized_fill [uninitialized.fill]

```
template<class NoThrowForwardIterator, class T>
void uninitialized_fill(NoThrowForwardIterator first, NoThrowForwardIterator last, const T& x);
```

Effects: Equivalent to:

```
for (; first != last; ++first)
    ::new (voidify(*first))
        typename iterator_traits<NoThrowForwardIterator>::value_type(x);
```

```
namespace ranges {
template<no-throw-forward-iterator I, no-throw-sentinel<I> S, class T>
    requires constructible_from<iter_value_t<I>, const T&>
I uninitialized_fill(I first, S last, const T& x);
template<no-throw-forward-range R, class T>
    requires constructible_from<range_value_t<R>, const T&>
borrowed_iterator_t<R> uninitialized_fill(R&& r, const T& x);
}
```

Effects: Equivalent to:

```
for (; first != last; ++first) {
    ::new (voidify(*first)) remove_reference_t<iter_reference_t<I>>(x);
}
return first;
```

```
template<class NoThrowForwardIterator, class Size, class T>
NoThrowForwardIterator uninitialized_fill_n(NoThrowForwardIterator first, Size n, const T& x);
```

Effects: Equivalent to:

```
for (; n--; ++first)
    ::new (voidify(*first))
        typename iterator_traits<NoThrowForwardIterator>::value_type(x);
return first;
```

```
namespace ranges {
template<no-throw-forward-iterator I, class T>
    requires constructible_from<iter_value_t<I>, const T&>
I uninitialized_fill_n(I first, iter_difference_t<I> n, const T& x);
}
```

Effects: Equivalent to:

```
return uninitialized_fill(counted_iterator(first, n), default_sentinel, x).base();
```

## 25.11.8 construct_at [specialized.construct]

```
template<class T, class... Args>
constexpr T* construct_at(T* location, Args&&... args);
```

```
namespace ranges {
template<class T, class... Args>
constexpr T* construct_at(T* location, Args&&... args);
}
```

Constraints: The expression `::new (declval<void*>()) T(declval<Args>()...)` is well-formed when treated as an unevaluated operand.

Effects: Equivalent to:

```
return ::new (voidify(*location)) T(std::forward<Args>(args)...);
```

## 25.11.9 destroy [specialized.destroy]

```
template<class T>
constexpr void destroy_at(T* location);
```
