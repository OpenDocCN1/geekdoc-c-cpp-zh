```
template <typename Value>
class vector
{
    // ...
    template <std::ranges::forward_range Range>
    vector(Range& r)
    : vector(begin(forward<Range>(r)),
             end(forward<Range>(r))) {}
};
```