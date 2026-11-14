```
```cpp
namespace views {
struct enumerate_t
{
    template <typename Range>
    enumerate_view<Range> operator()(Range&& r) const
noexcept
{
    return enumerate_view <Range>
{std::forward<Range>(r) };
};
static constexpr enumerate_t enumerate;
}
for (auto [i, value] : views::enumerate(seq))
cout << "The " << i << "th value is " << value << endl;
```
```

Of course, we also want the pipe operator for our view:

Click here to view code image

```
```cpp
namespace views {
template <typename Range>
enumerate_view <Range> operator|(Range&& r, enumerate_t)
noexcept
{
    return enumerate_view <Range>{std::forward<Range>(r)
(r) ;
}
for (auto [i, value] : seq | views::enumerate)
cout << "The " << i << "th value is " << value << endl;
```
```

A full-fledged production code of this will contain more details like a richer iterator interface and some type declarations about its behavior but the fundamental behavior is already provided in our minimalist implementation. After realizing how simple this was, the author regrets not having done this much earlier. This said, we invite you to implement your own ranges whenever this helps. As mentioned before, the iterators are an ingenious idea to maximize applicability but it shouldn’t be the primary interface to work with on the application level.

# C++17 4.1.6 Parallel Computation