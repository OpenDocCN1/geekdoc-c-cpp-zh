![](bbox=[0.13, 0.115, 0.21, 0.17])

# # Class Template Argument Deduction Guide

Since C++17, the compiler can deduce template parameters from template arguments. The template deduction guide is a pattern for the compiler to deduce the template arguments.

When you use ContainerView(myVec), the compiler applies the following user-defined deduction guide:

```
**User-Defined Deduction Guide for ContainerView**
~~~cpp
template <class Range>
ContainerView(Range&& range) -> ContainerView<std::ranges::views::all_t<Range>>;
~~~
```

Essentially, a call ContainerView(myVec) causes the compiler to instantiate the code on the right of the arrow ->:

```
**Applying the deduction guide for ContainerView(myVec)**
~~~cpp
ContainerView<std::ranges::views::all_t<std::vector<int>>>{myVec};
~~~
```

cppreference.com[^12] provides more information to the user-defined deduction guide for class templates.

# ## 5.1.7.3 A TrimByView

When you study the previous example containerView.cpp, you notice that the member functions begin and end are crucial for implementing a new view. The following view, TrimByView, adjusts the view's boundaries by ignoring its range's beginning and trailing count elements.

```
**Creating a view from a container excluding the beginning and trailing count elements**
~~~cpp
1  // trimByView.cpp
2
3  #include <iostream>
4  #include <ranges>
5  #include <string>
6  #include <vector>
7
8  template<std::ranges::input_range Range>
9  requires std::ranges::view<Range>
10 class TrimByView : public std::ranges::view_interface<TrimByView<Range>> {
11 private:
12   Range range_{};
13   std::ranges::iterator_t<Range> begin_{ std::begin(range_) };
14   std::ranges::iterator_t<Range> end_{ std::end(range_) };
~~~
```

[^12]: https://en.cppreference.com/w/cpp/language/class_template_argument_deduction