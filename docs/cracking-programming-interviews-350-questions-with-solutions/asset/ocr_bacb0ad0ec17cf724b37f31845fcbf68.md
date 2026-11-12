# ### 1.9. Fixed size generic array in C++

```
```cpp
{
    return !(x == y);
}

template <class ElementType, size_t N>
inline bool
operator<(const array<ElementType, N>& x, const
    array<ElementType, N>& y)
{
    return std::lexicographical_compare(x.elements,
        x.elements + N, y.elements, y.elements + N);
}

template <class ElementType, size_t N>
inline bool
operator>(const array<ElementType, N>& x, const
    array<ElementType, N>& y)
{
    return y < x;
}

template <class ElementType, size_t N>
inline bool
operator<=(const array<ElementType, N>& x, const
    array<ElementType, N>& y)
{
    return !(y < x);
}

template <class ElementType, size_t N>
inline bool
operator>=(const array<ElementType, N>& x, const
    array<ElementType, N>& y)
{
    return !(x < y);
}

template <class ElementType, size_t N>
swap(const array<ElementType, N>& x, const array<
    ElementType, N>& y)
{
    x.swap(y);
}

template <size_t Index, class ElementType, size_t N>
inline ElementType&
get(array<ElementType, N>& a)
{
    static_assert(Index < N, "Index_out_of_bounds
        in std::get<> (std::array)");
    return a[Index];
}
```
```