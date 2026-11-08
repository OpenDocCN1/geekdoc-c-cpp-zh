
```
19      std::cout << "vec == vec2: " << (vec == vec2) << '\n';
20
21      for (int i : vec) std::cout << i << " ";
22
23  }
```

The first iota call (line 15) creates all numbers from 0 to 9, incremented by 1. The second iota call (line 17) creates an infinite data stream, starting with 0, incremented by 1. std::views::iota(0) is lazy. I only get a new value if I ask for it. I ask for it ten times. Consequently, both vectors are identical.

```
vec == vec2: true
0 1 2 3 4 5 6 7 8 9
```

Using std::views::iota to fill a std::vector

Now, I want to solve a small challenge: finding the first 20 prime numbers starting with 1,000,000.

## The first 20 prime numbers starting with 1'000'000

```
1   // rangesLazy.cpp
2
3   #include <iostream>
4   #include <ranges>
5
6
7   bool isPrime(int i) {
8       for (int j=2; j*j <= i; ++j){
9           if (i % j == 0) return false;
10      }
11      return true;
12  }
13
14  int main() {
15
16      std::cout << "Numbers from 1'000'000 to 1'001'000 (displayed each 100th): "
17                << '\n';
18      for (int i: std::views::iota(1'000'000, 1'001'000)) {
19          if (i % 100 == 0) std::cout << i << " ";
20      }
21
22      std::cout << "\n\n";
23
24      auto odd = [](int i){ return i % 2 == 1; };
25      std::cout << "Odd numbers from 1'000'000 to 1'001'000 (displayed each 100th): "
26                << '\n';
for (int i: std::views::iota(1'000'000, 1'001'000) | std::views::filter(odd)) {
    if (i % 100 == 1) std::cout << i << " ";
}

std::cout << "\n\n";

std::cout << "Prime numbers from 1'000'000 to 1'001'000: " << '\n';
for (int i : std::views::iota(1'000'000, 1'001'000) | std::views::filter(odd)
                                             | std::views::filter(isPrime)) {
    std::cout << i << " ";
}

std::cout << "\n\n";

std::cout << "20 prime numbers starting with 1'000'000: " << '\n';
for (int i : std::views::iota(1'000'000) | std::views::filter(odd)
                                          | std::views::filter(isPrime)
                                          | std::views::take(20)) {
    std::cout << i << " ";
}

std::cout << '\n';
```

This is my iterative strategy:

- **line 18:** Of course, I don’t know when I have 20 primes greater than 1000000. To be on the safe side, I create 1000 numbers. For obvious reasons, I displayed only each 100th.
- **line 27:** I’m only interested in the odd numbers; therefore, I remove the even numbers.
- **line 34:** Now, it’s time to apply the next filter. The predicate isPrime (line 7) returns if a number is prime. As you can see in the following screenshot, I was too eager. I got 75 primes.
- **line 42:** Laziness is a virtue. I use std::views::iota as an infinite number factory, starting with 1000000 and ask precisely for 20 primes.

## 5.1.7 Define a View

You can define your view.

### 5.1.7.1 `std::ranges::view_interface`

Thanks to the `std::ranges::view_interface` helper class, defining a view is easy. To fulfill the concept view, your view needs at least a default constructor, and member functions `begin()` and `end()`:

Your own view

```cpp
class MyView : public std::ranges::view_interface<MyView> {
public:
    auto begin() const { /*...*/ }
    auto end() const { /*...*/ }
};
```

By deriving MyView public from the helper class `std::ranges::view_interface` using itself as a template parameter, MyView becomes a view. This technique of class template having itself as a template parameter is called [Curiously Recurring Template Pattern](https://en.wikipedia.org/wiki/Curiously_recurring_template_pattern) (short CRTP).

I use this technique in the next example to create a view out of a container of the Standard Template Library.

### 5.1.7.2 A Container View

The view `ContainerView` creates a view on an arbitrary container.

Creating a view from a container

```cpp
// containerView.cpp

#include <iostream>
#include <ranges>
#include <string>
#include <vector>

template<std::ranges::input_range Range>
requires std::ranges::view<Range>
class ContainerView : public std::ranges::view_interface<ContainerView<Range>> {
private:
    Range range_{};
    std::ranges::iterator_t<Range> begin_{ std::begin(range_) };
    std::ranges::iterator_t<Range> end_{ std::end(range_) };
15
16 public:
17     ContainerView() = default;
18
19     constexpr ContainerView(Range r) : range_(std::move(r)) ,
20                                     begin_(std::begin(r)), end_(std::end(r)) {}
21
22     constexpr auto begin() const {
23         return begin_;
24     }
25     constexpr auto end() const {
26         return end_;
27     }
28 };
29
30 template <typename Range>
31 ContainerView(Range&& range) -> ContainerView<std::ranges::views::all_t<Range>>;
32
33 int main() {
34
35     std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9};
36
37     auto myContainerView = ContainerView(myVec);
38     for (auto c : myContainerView) std::cout << c << " ";
39     std::cout << '\n';
40
41     for (auto i : std::views::reverse(ContainerView(myVec))) std::cout << i << ' ';
42     std::cout << '\n';
43
44     for (auto i : ContainerView(myVec) | std::views::reverse) std::cout << i << ' ';
45     std::cout << '\n';
46
47     std::cout << '\n';
48
49     std::string myStr = "Only for testing purpose.";
50
51     auto myContainerView2 = ContainerView(myStr);
52     for (auto c : myContainerView2) std::cout << c << " ";
53     std::cout << '\n';
54
55     for (auto i : std::views::reverse(ContainerView(myStr))) std::cout << i << ' ';
56     std::cout << '\n';
57
58     for (auto i : ContainerView(myStr) | std::views::reverse) std::cout << i << ' ';
59     std::cout << '\n';
}
```

The class template ContainerView (line 8) derives from the helper class std::ranges::view_interface and requires that the container support the concept std::ranges::view (line 9). The remaining, minimal implementation is straightforward. ContainerView has a default constructor (line 17). Due to a change in the C++20 standard for a view, this default constructor is not necessary anymore, but many compilers still require it. On the contrary, the two member functions begin() (line 22) and end() (line 25) are required. Initially, a view must be default constructible. This requirement was removed, but many compilers still require a default constructor. Therefore, ContainerView has one. For convenience, I added a user-defined deduction guide for class template argument deduction (line 32).

In the main function, I apply the ContainerView on a std::vector (line 37) and a std::string (line 49) and iterate through them forwards and backward.

![](img/c60a87adb7f61e2e82071d081bbb389a_273_0.png)

Creating a view from a container

Let me add a few words to the class template argument deduction guide.

![](img/c60a87adb7f61e2e82071d081bbb389a_274_0.png)

### Class Template Argument Deduction Guide

Since C++17, the compiler can deduce template parameters from template arguments. The template deduction guide is a pattern for the compiler to deduce the template arguments.

When you use ContainerView(myVec), the compiler applies the following user-defined deduction guide:

**User-Defined Deduction Guide for ContainerView**

```cpp
template <class Range>
ContainerView(Range&& range) -> ContainerView<std::ranges::views::all_t<Range>>;
```

Essentially, a call ContainerView(myVec) causes the compiler to instantiate the code on the right of the arrow ->:

**Applying the deduction guide for ContainerView(myVec)**

```cpp
ContainerView<std::ranges::views::all_t<std::vector<int>>>{myVec};
```

cppreference.com[^12] provides more information to the user-defined deduction guide for class templates.

### 5.1.7.3 A TrimByView

When you study the previous example containerView.cpp, you notice that the member functions begin and end are crucial for implementing a new view. The following view, TrimByView, adjusts the view's boundaries by ignoring its range's beginning and trailing count elements.

**Creating a view from a container excluding the beginning and trailing count elements**

```cpp
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
```

[^1]: https://www.modernescpp.com/index.php/c-is-still-lazy

[^12]: https://en.cppreference.com/w/cpp/language/class_template_argument_deduction
