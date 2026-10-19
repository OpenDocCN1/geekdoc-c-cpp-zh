```
constexpr iterator<true> begin() const
  requires range<const V> &&
           regular_invocable<const F&, range_reference_t<const V>>;

3    *Effects:* Equivalent to:

         return iterator<true>{*this, ranges::begin(base_)};

constexpr sentinel<false> end();

4    *Effects:* Equivalent to:

         return sentinel<false>{ranges::end(base_)};

constexpr iterator<false> end() requires common_range<V>;

5    *Effects:* Equivalent to:

         return iterator<false>{*this, ranges::end(base_)};

constexpr sentinel<true> end() const
  requires range<const V> &&
           regular_invocable<const F&, range_reference_t<const V>>;

6    *Effects:* Equivalent to:

         return sentinel<true>{ranges::end(base_)};

constexpr iterator<true> end() const
  requires common_range<const V> &&
           regular_invocable<const F&, range_reference_t<const V>>;

7    *Effects:* Equivalent to:

         return iterator<true>{*this, ranges::end(base_)};
```

# 24.7.6.3  Class template `transform_view::iterator`

```
namespace std::ranges {
  template<input_range V, copy_constructible F>
    requires view<V> && is_object_v<F> &&
             regular_invocable<F&, range_reference_t<V>> &&
             can-reference<invoke_result_t<F&, range_reference_t<V>>>
  template<bool Const>
  class transform_view<V, F>::iterator {
  private:
    using Parent =                         // exposition only
      conditional_t<Const, const transform_view, transform_view>;
    using Base   =                         // exposition only
      conditional_t<Const, const V, V>;
    iterator_t<Base> current_ =            // exposition only
      iterator_t<Base>();
    Parent* parent_ = nullptr;              // exposition only
  public:
    using iterator_concept = see below;
    using iterator_category = see below;
    using value_type =
      remove_cvref_t<invoke_result_t<F&, range_reference_t<Base>>>;
    using difference_type = range_difference_t<Base>;

    iterator() = default;
    constexpr iterator(Parent& parent, iterator_t<Base> current);
    constexpr iterator(iterator<!Const> i)
      requires Const && convertible_to<iterator_t<V>, iterator_t<Base>>;

    constexpr iterator_t<Base> base() const &
      requires copyable<iterator_t<Base>>;
    constexpr iterator_t<Base> base() &&;
    constexpr decltype(auto) operator*() const
      { return invoke(*parent_->fun_, *current_); }
```