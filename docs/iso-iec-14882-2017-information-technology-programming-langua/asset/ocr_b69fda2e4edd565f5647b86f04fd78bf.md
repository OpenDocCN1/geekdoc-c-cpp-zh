# ISO/IEC 14882:2017(E)

```
template <T> inline constexpr bool is_move_assignable_v
    = is_move_assignable<T>::value;
template <T, class U> inline constexpr bool is_swappable_with_v
    = is_swappable<T, U>::value;
template <T> inline constexpr bool is_swappable_v
    = is_swappable<T>::value;
template <T> inline constexpr bool is_destructible_v
    = is_destructible<T>::value;
template <T, class Args...> inline constexpr bool is_trivially_constructible_v
    = is_trivially_constructible<T, Args...>::value;
template <T> inline constexpr bool is_trivially_default_constructible_v
    = is_trivially_default_constructible<T>::value;
template <T> inline constexpr bool is_trivially_copy_constructible_v
    = is_trivially_copy_constructible<T>::value;
template <T> inline constexpr bool is_trivially_move_constructible_v
    = is_trivially_move_constructible<T>::value;
template <T, class Args...> inline constexpr bool is_trivially_assignable_v
    = is_trivially_assignable<T, Args...>::value;
template <T> inline constexpr bool is_trivially_copy_assignable_v
    = is_trivially_copy_assignable<T>::value;
template <T> inline constexpr bool is_trivially_move_assignable_v
    = is_trivially_move_assignable<T>::value;
template <T> inline constexpr bool is_trivially_destructible_v
    = is_trivially_destructible<T>::value;
template <T, class Args...> inline constexpr bool is_not_constructible_v
    = is_not_constructible<T, Args...>::value;
template <T, class Args...> inline constexpr bool is_not_default_constructible_v
    = is_not_default_constructible<T, Args...>::value;
template <T> inline constexpr bool is_not_copy_constructible_v
    = is_not_copy_constructible<T>::value;
template <T> inline constexpr bool is_not_move_constructible_v
    = is_not_move_constructible<T>::value;
template <T, class Args...> inline constexpr bool is_not_assignable_v
    = is_not_assignable<T, Args...>::value;
template <T> inline constexpr bool is_not_move_assignable_v
    = is_not_move_assignable<T>::value;
template <T> inline constexpr bool is_not_copy_assignable_v
    = is_not_copy_assignable<T>::value;
template <T, class Args...> inline constexpr bool is_not_swappable_with_v
    = is_not_swappable_with<T, Args...>::value;
template <T> inline constexpr bool is_not_swappable_v
    = is_not_swappable<T>::value;
template <T> inline constexpr bool is_not_destructible_v
    = is_not_destructible<T>::value;
template <T> inline constexpr bool has_virtual_destructor_v
    = has_virtual_destructor<T>::value;
template <T> inline constexpr bool has_unique_object_representations_v
    = has_unique_object_representations<T>::value;

// 23.5.5. type properties */
template <T> inline constexpr size_t alignment_of_v
    = alignment_of<T>::value;
template <T> inline constexpr size_t rank_v
    = rank<T>::value;
template <T, unsigned int I = 0> inline constexpr size_t extent_v
```