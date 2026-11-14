incremented to equal last. This shouldn't affect the data that we copy afterward. To guarantee this, we need a forward_iterator. Now we can initialize a vector for instance with the data of a list:

Click here to view code image

```
std::list<1> {17, 4, 3, 9, 2};
dmc::vector<int> v(begin(l), end(l));
```

If we omitted the vector's value type we would get a vector of iterators. Unless we provide an appropriate deduction guide:

Click here to view code image

```
template <std::forward_iterator Iter >
vector(Iter first, Iter last) -> vector
>std::iter_value_t<Iter> >;
```

Our new constructor shall require a forward_range and reuse the preceding one:

Click here to view code image

```
template <typename Value>
class vector
{
    // ...
    template <std::ranges::forward_range Range>
    vector (Range&& r)
    : vector (begin(forward<Range>(r)),
    end(forward<Range>(r))) {}
};
```

A forward_range is a range whose begin function returns a forward_iterator. We will say more about ranges in Section 4.1.5. For now we can just think of ranges as types with an appropriate begin and end that applies to all standard containers but is not limited to it.

In contrast to the discussion we just entered, the implementation is quite simple: the range is passed as the forward reference and the actual initialization is delegated to the iterator-pair constructor. If the value type of vector shall be deduced we need the according guide:

Click here to view code image

```
template <std::ranges::forward_range Range>
vector (Range&& r)
```