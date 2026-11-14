
where w is resized to the size of v. This interface is not provided by the standard library and we will implement it now.

To adapt the size of the target to that of the source we must add two extra requirements: the source must provide the size information and the target must be able to change its size. The source’s size can always be determined with the iterator function distance but it might be expensive (up to linear complexity) and could invalidate the starting iterator when the type is not a forward_iterator. The range library introduces the concept sized_range for ranges with size function of constant complexity. This concept covers our requirements for the source. Those of the target must be realized in a new concept:

```cpp
template <typename R>
concept ResizableRange =
    ranges::range<R> &&
    requires(R& r, size_t n)
    {
        r.resize(n);
    };
```

Now we can write a reliable copy function:

Click here to view code image

```cpp
template <sized_range Source, ResizableRange Target>
auto copy(const Source& src, Target& tgt)
{
    tgt.resize(size(src));
    return copy(src, begin(tgt));
}
```

When all copy overloads are properly constrained, our implementation doesn’t cause any ambiguity. A disadvantage of this implementation was pointed out by Sean Parent: objects are default-constructed during a prolonging resize and then overwritten anyway. To avoid this overhead or compile errors for classes without a default constructor, we better use clear and reserve before copying with a back_insert_iterator:

Click here to view code image

```cpp
template <typename R>
concept ExpandableRange =
    ranges::range<R> &&
    requires(R& r, size_t n)
{
    r.reserve(n);
};
template <sized_range Source, ExpandableRange Target>
auto copy(const Source& src, Target& tgt)
{
    tgt.clear();
    tgt.reserve(ranges::size(src));
    return ranges::copy(src, back_insert_iterator(tgt));
}
```

In a similar fashion, many standard functions can now be realized with a range for each iterator pair or single iterator. This establishes an interface that is more convenient and more reliable at the same time.

## 4.1.5.3 Standard Views

=> c++20/ranges_iota.cpp

All standard containers contain a begin and an end function that return iterators and are therefore ranges. Ranges are however not limited to containers; their definition is more generic. A range does not necessarily contain data. For instance, iterating over a view named `iota` is equivalent to reading data from a container with ascending data:

Click here to view code image

```cpp
for (int i : views::iota(1, 10))
    cout << i << endl;
```

This snippet prints the values from 1 to 9 as if we iterated over a container containing those values. The view is similar to the `irange` class we introduced in Section 2.7.6.

=> c++20/ranges_examples.cpp

Most views establish a new perspective on a given container or another range without creating new containers. To select from a given range only those entries that hold a certain criterion, we can use the `filter` view. Unfortunately, most view classes require another view as the argument and aren’t applicable to arbitrary ranges. Therefore, it’s not advisable to use them directly. Instead we should use the corresponding `Range Adaptor`. For each view class there exists an according adaptor in the sub-namespace views. For instance, views::filter is the adaptor to the class filter_view. Say we want to print the values from a vector that are larger than 4 and smaller than 7:

Click here to view code image

```cpp
bool in_range(int i) { return i > 4 && i < 7; }
vector<int> seq = {3, 4, 7, 6, 9, 2, 5, 7, 8};
for (int i : views::filter(seq, in_range))
    cout << i << " is in range.\n";
```

In this loop, only the numbers in_range are printed and the others skipped. views::filter doesn't create a new container but only a lightweight proxy on seq. The iterators of filter are merely wrappers for those of the underlying iterator (in this case vector). To see the filtered values in seq, the iterator increment of filter repeats the increment of the vector iterator until the referred value holds the filter condition. Another useful view is transform, which applies a unary function to every entry:

Click here to view code image

```cpp
auto square = [](int n) { return n * n; };
for (int i : views::transform(views::filter(seq, in_range),
                                  square))
    cout << i << " is the squared value of an in-range
    entry.\n";
```

Here we square all values from seq that are larger than 4 and smaller than 7. We can also see in this example that nesting views doesn't lead to particularly readable code. To improve the readability, the views provide a pipe operator similar to that of shells in Unix. In this case we omit the range argument in the adaptor:

Click here to view code image

```cpp
for (int i : seq | views::filter(in_range)
                 | views::transform(square))
    cout << i << " is the squared value of an in-range
    entry.\n";
```

Another generalization of ranges is that begin and end may return different types since the end iterator is only used for comparison. Actually, the object returned by `end` doesn't need to be an iterator but only a so-called *Sentinel*. This can be any type as long as it is comparable with the according iterator.

Using sentinels has some impact on algorithms. The range-based `for` loop was already generalized in C++17 to enable different types between `begin` and `end`. Classical STL algorithms are designed for pairs of iterators. To call them with arbitrary ranges we can use the `common` view. For instance, a range-based sort function could be implemented as follows:

Click here to view code image

```cpp
template <random_access_range Range>
void sort(Range& r)
{
    auto cr(views::common(r));
    sort(begin(cr), end(cr));
}
```

A view that doesn't seem very useful at the first glance but turned out to be convenient is `all`: it's just a view on a range representing the same content. However, range views have output operators<sup>4</sup> in contrast to some container types and we can use it therefore for printing:

```cpp
cout << "seq = " << views::all(seq) << endl;
```

4. At least in the prototype.

Furthermore, `views::all` is used internally by the other views to turn an arbitrary range into a view. In Table 4-2, you'll find a survey of the views introduced in C++20.

## 4.1.5.4 Writing Our Own View

=> c++20/range_enumerate_example.cpp

One view of Eric Niebler's prototype implementation that didn't make it into the standard is `enumerate`. This view provides us for each entry in the range with a position and a value. The author used this quite frequently in Python programs and is therefore now longing to have it in C++ as well.

### Table 4-2: Range views

| Adaptor name | Semantics |
| :--- | :--- |
| views::all | All entries in the range |
| views::filter | Entries that hold a given property |
| views::transform | Apply a function to each entry |
| views::iota | Iterate over a range of integers |
| views::take | Take n entries from a range |
| views::join | Joins a sequence of ranges into one range |
| views::empty | Creates a range of a given value type without entries |
| views::single | Creates a range with a given single entry |
| views::split | Splits a range into sub-ranges for a given delimiter |
| views::counted | Creates a range of n entries starting with a given iterator |
| views::common | Establishes a range where begin and end have the same type |
| views::reverse | Traverses a given range in reverse order |

For simplicity we assume that the enumerated range is not an rvalue and doesn't need to be stored. We further assume that begin and end return the same type. Then the view itself is quite simple:

Click here to view code image

```cpp
template <typename Range>
class enumerate_view
{
    using iter = enumerate_iterator<Range>;
public:
    enumerate_view(Range& r) : r(r) {}
    iter begin() const noexcept { return iter{0, std::begin(r)}; }
    iter end() const noexcept { return iter{-1, std::end(r)}; }
};
```
