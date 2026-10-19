# ISO/IEC 14882:2020(E)

Effects: Initializes begin_ with std::move(i) and end_ with s. If StoreSize is true, initializes size_ with n.

> [Note 1: Accepting the length of the range and storing it to later return from size() enables subrange to model sized_range even when it stores an iterator and sentinel that do not model sized_sentinel_for. — end note]

```
template<not-same-as<subrange> R>
    requires borrowed_range<R> &&
        convertible-to-non-slicing<iterator_t<R>, I> &&
        convertible_to<sentinel_t<R>, S>
constexpr subrange(R&& r) requires (!StoreSize || sized_range<R>);
```

Effects: Equivalent to:

+   — If StoreSize is true, subrange{r, ranges::size(r)}.
+   — Otherwise, subrange{ranges::begin(r), ranges::end(r)}.

```
template<not-same-as<subrange> PairLike>
    requires pair-like-convertible-from<PairLike, const I&, const S&>
constexpr operator PairLike() const;
```

Effects: Equivalent to: return PairLike(begin_, end_);

# 24.5.4.3 Accessors [range.subrange.access]

```
constexpr I begin() const requires copyable<I>;
```

Effects: Equivalent to: return begin_;

```
[[nodiscard]] constexpr I begin() requires (!copyable<I>);
```

Effects: Equivalent to: return std::move(begin_);

```
constexpr S end() const;
```