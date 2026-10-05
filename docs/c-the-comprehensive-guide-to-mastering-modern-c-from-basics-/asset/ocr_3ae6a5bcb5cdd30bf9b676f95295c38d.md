```
// https://godbolt.org/z/veovKc8KJ
// as before ...
auto out = in
views::filter([](const int i) { return i%3 == 0; });
views::transform([](const int i) { return i*i; });
vector<int> result(from_range, out);
```

**Listing 24.7** *The range marker also exists only since C++23.*

# 24.1.7 Ranges, Views, Concepts, Adapters, Generators, and Algorithms

The ranges library is located in the <ranges> header, contains the std::ranges namespace, and is divided into several areas:

+   - Ranges
nA range is essentially anything that can be iterated over, has a start, and potentially an end, called a sentinel. A typical range is based on a data area—for example, a container—and you can also modify the elements through the range.

+   - Views
A view is a range and is defined by operations it wants to perform on the elements, such as filtering or transforming the elements. Views are lazy, performing operations only when necessary.

+   - Concepts
The ranges library defines, for example, the input_range concept, which you can use in function parameters.

+   - Converter
If you use ranges::to (C++23), a view is converted into