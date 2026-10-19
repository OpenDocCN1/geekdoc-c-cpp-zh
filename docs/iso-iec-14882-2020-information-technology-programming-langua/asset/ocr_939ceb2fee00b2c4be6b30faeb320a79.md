# 24.7.14.2 Class template common_view [range.common.view]

— end example]

```
namespace std::ranges {
    template<view V>
        requires (!common_range<V> && copyable<iterator_t<V>>)
    class common_view : public view_interface<common_view<V>> {
    private:
        V base_ = V();  // exposition only
    public:
        common_view() = default;

        constexpr explicit common_view(V r);

        template<viewable_range R>
            requires (!common_range<R> && constructible_from<V, views::all_t<R>>)
        constexpr explicit common_view(R&& r);

        constexpr V base() const& requires copy_constructible<V> { return base_; }
        constexpr V base() && { return std::move(base_); }

        constexpr auto begin() {
            if constexpr (random_access_range<V> && sized_range<V>)
                return ranges::begin(base_);
            else
                return common_iterator<iterator_t<V>, sentinel_t<V>>(ranges::begin(base_));
        }

        constexpr auto begin() const requires range<const V> {
            if constexpr (random_access_range<const V> && sized_range<const V>)
                return ranges::begin(base_);
            else
                return common_iterator<iterator_t<const V>, sentinel_t<const V>>(ranges::begin(base_));
        }

        constexpr auto end() {
            if constexpr (random_access_range<V> && sized_range<V>)
                return ranges::begin(base_) + ranges::size(base_);
            else
                return common_iterator<iterator_t<V>, sentinel_t<V>>(ranges::end(base_));
        }

        constexpr auto end() const requires range<const V> {
            if constexpr (random_access_range<const V> && sized_range<const V>)
                return ranges::begin(base_) + ranges::size(base_);
            else
                return common_iterator<iterator_t<const V>, sentinel_t<const V>>(ranges::end(base_));
        }

        constexpr auto size() requires sized_range<V> {
            return ranges::size(base_);
        }
        constexpr auto size() const requires sized_range<const V> {
            return ranges::size(base_);
        }
    };

    template<class R>
        common_view(R&&) -> common_view<views::all_t<R>>;
}
```