then T{ranges::begin(E), ranges::begin(E) + min<D>(ranges::size(E), F)}, except that E is evaluated only once.
(2.3) — Otherwise, ranges::take_view{E, F}.

3 [Example 1:

```
vector<int> is{0,1,2,3,4,5,6,7,8,9};
take_view few{is, 5};
for (int i : few)
    cout << i << ' '; // prints: 0 1 2 3 4
— end example
```

# 24.7.7.2 Class template take_view [range.take.view]

```
namespace std::ranges {
template<view V>
class take_view : public view_interface<take_view<V>> {
private:
    V base_ = V();                                 // exposition only
    range_difference_t<V> count_ = 0;              // exposition only
    // 24.7.7.3, class template take_view::sentinel
    template<bool> struct sentinel;                // exposition only
public:
    take_view() = default;
    constexpr take_view(V base, range_difference_t<V> count);

    constexpr V base() const& requires copy_constructible<V> { return base_; }
    constexpr V base() && { return std::move(base_); }

    constexpr auto begin() requires (!simple-view<V>) {
        if constexpr (sized_range<V>) {
            if constexpr (random_access_range<V>)
                return ranges::begin(base_);
            else {
                auto sz = size();
                return counted_iterator{ranges::begin(base_), sz};
            }
        } else
            return counted_iterator{ranges::begin(base_), count_};
    }

    constexpr auto begin() const requires range<const V> {
        if constexpr (sized_range<const V>) {
            if constexpr (random_access_range<const V>)
                return ranges::begin(base_);
            else {
                auto sz = size();
                return counted_iterator{ranges::begin(base_), sz};
            }
        } else
            return counted_iterator{ranges::begin(base_), count_};
    }

    constexpr auto end() requires (!simple-view<V>) {
        if constexpr (sized_range<V>) {
            if constexpr (random_access_range<V>)
                return ranges::begin(base_) + size();
            else
                return default_sentinel;
        } else
            return sentinel<false>{ranges::end(base_)};
    }
}
```