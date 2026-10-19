```
```cpp
template<size_t I, class... Types>
  constexpr const variant_alternative_t<I, variant<Types...>>& get(const variant<Types...>&);
template<size_t I, class... Types>
  constexpr const variant_alternative_t<I, variant<Types...>>&& get(const variant<Types...>&&);

template<class T, class... Types>
  constexpr T& get(variant<Types...>&);
template<class T, class... Types>
  constexpr T&& get(variant<Types...>&&);
template<class T, class... Types>
  constexpr const T& get(const variant<Types...>&);
template<class T, class... Types>
  constexpr const T&& get(const variant<Types...>&&);

template<size_t I, class... Types>
  constexpr add_pointer_t<variant_alternative_t<I, variant<Types...>>>
    get_if(variant<Types...>*) noexcept;
template<size_t I, class... Types>
  constexpr add_pointer_t<const variant_alternative_t<I, variant<Types...>>>
    get_if(const variant<Types...>*) noexcept;

template<class T, class... Types>
  constexpr add_pointer_t<T>
    get_if(variant<Types...>*) noexcept;
template<class T, class... Types>
  constexpr add_pointer_t<const T>
    get_if(const variant<Types...>*) noexcept;

// 20.7.6, relational operators
template<class... Types>
  constexpr bool operator==(const variant<Types...>&, const variant<Types...>&);
template<class... Types>
  constexpr bool operator!=(const variant<Types...>&, const variant<Types...>&);
template<class... Types>
  constexpr bool operator<(const variant<Types...>&, const variant<Types...>&);
template<class... Types>
  constexpr bool operator>(const variant<Types...>&, const variant<Types...>&);
template<class... Types>
  constexpr bool operator<=(const variant<Types...>&, const variant<Types...>&);
template<class... Types>
  constexpr bool operator>=(const variant<Types...>&, const variant<Types...>&);
template<class... Types> requires (three_way_comparable<Types> && ...)
  constexpr common_comparison_category_t<compare_three_way_result_t<Types>...>
    operator<=>(const variant<Types...>&, const variant<Types...>&);

// 20.7.7, visitation
template<class Visitor, class... Variants>
  constexpr see below visit(Visitor&&, Variants&&...);
template<class R, class Visitor, class... Variants>
  constexpr R visit(Visitor&&, Variants&&...);

// 20.7.8, class monostate
struct monostate;

// 20.7.9, monostate relational operators
constexpr bool operator==(monostate, monostate) noexcept;
constexpr strong_ordering operator<=>(monostate, monostate) noexcept;

// 20.7.10, specialized algorithms
template<class... Types>
  void swap(variant<Types...>&, variant<Types...>&) noexcept(see below);

// 20.7.11, class bad_variant_access
class bad_variant_access;
```
```