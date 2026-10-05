
```cpp
auto no = numbers.find(30);
if(no == numbers.end()) { std::cout << "not there.\n"; }
auto yes = numbers.find(20);
if(yes != numbers.end()) { std::cout << *yes << "\n"; }
```

## 24.1.6 Ranges Simplify Iterators

To understand containers, you can avoid iterators. They are not difficult; they abstract pointers from the basic idea. However, iterators can be associated with additional functionalities and properties; how they are incremented, whether they allow random access, and so on. This provides a clear interface to algorithms, which we will discuss shortly. But they also have their weaknesses. For nearly 30 years, we have lived with them, and improvements have been worked on for a long time. Since C++20, one such improvement has arrived: ranges.

Ranges are a new way to define ranges of elements. They are not limited to containers. However, when it comes to containers, they bundle the two iterators that are always needed together. This can be problematic; for example, if you accidentally mix begin() and end() from two different containers, the compiler will not notice. Ranges passed as a single parameter. This is not only a simplification but also a unification, as ranges combine the following types of ranges into one concept:

- first and (exclusive) last
- Range between two iterators, as containers provide with begin() and end().

- first and size
- A range *from* an iterator with a specific length, typical for C-arrays.

- first and a predicate
- Something like `<iostream>`, such as `istream_iterator`, which reads elements from a stream until a certain predicate is met.

- first and ...
- Generators like `iota()` from `<numeric>`, which produces an endless sequence of elements.

A range can represent all of this. And in some cases, we don't need to know which of these variants underlies a given range. When you browse the documentation, you will encounter the term *sentinel*. This is the generalization of the `end()` iterator and is part of the range definition. The technical difference between `end()` of containers and the sentinel or ranges is that the sentinel does not have to be of the same type as the `begin()` of the range.

A typical example is `\0` at the end of C strings or the EOF in files. If you want to classically map an iterator `end()` for these cases, you first have to run to the end of the container. This is not only inefficient but also impractical for EOF in files. In the concept of the sentinel, this now abstractly reads as "until \0" or "until EOF."

## Spans Are Different from Ranges

For contiguous containers like string and vector, simpler variants of views are possible: string_view existed since C++20, and span added with C++23. These should not be confused with ranges. However, span is also borrowed_range and therefore compatible in many places.

## Combining Views and Pipelines

But that's not all. With ranges, views were introduced. Are you coming from Java? Do you like streams? Functional programming? Then you'll love views. Views are ranges that do not store elements but access other ranges. So they are something like a "perspective" on other ranges. And pipelines are a way to combine views. With the pipe operator |, you create and combine views. We will get more specific about algorithms in a moment, but I want to briefly show you what a pipeline of views looks like. The next listing shows how this previously looked with algorithms.

```cpp
// https://godbolt.org/z/arfee
using namespace std;
vector<int> in = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
vector<int> tmp;
vector<int> out;
copy_if(in.begin(), in.end(), back_inserter(tmp), [](int i) { return i % 3 == 0; });

transform(tmp.begin(), tmp.end(), back_inserter(out), [](int i) { return i*i; });
```

In the next one, you can see that algorithm after another is significantly more elegant with a pipeline of views.

```cpp
// https://godbolt.org/z/tg10d
using namespace std;
namespace views = std::ranges::views;
vector<int> in = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
auto out = in
| views::filter([](int i) { return i%3 == 0; })
| views::transform([](int i) { return i*i; });
```

## A pipeline of views instead of algorithms

With the first |, I create a view into the container. The filter adapter creates another view that only allows elements that satisfy the predicate. None of the views store elements. They are just views on the elements of the container. The second | combines this view with the transform adapter—a computation on the individual elements. Even the out variable is initially a view, and you should output or process it as it does not contain real elements. This is important because the preceding snippet calculates nothing. Views behave in a lazy manner: only when you query the elements of out are the computations performed.

## C++23 and Ranges

With C++23, the standard library has received a massive extension of ranges. You get many more ranges and views to combine. Ultimately, starting with C++23, working with ranges becomes truly enjoyable. I will point out elements from C++23 in the book.

Without C++23, you either use a loop or iterators to materialize the elements of a view—for example, to store them in a container:

```cpp
vector result(out.begin(), out.end());
```

As you can see, in C++20, you even have to resort to the iterators of the view to fill the container. Starting with C++23, you can also use ranges::to within the pipeline for this.

```cpp
// https://godbolt.org/z/EdYzfEM
// as before
auto out = in
| views::filter([](const int i) { return i%3 == 0; })
| views::transform([](const int i) { return i*i; })
| std::ranges::to<vector>;
```

## With C++23, you can use ranges::to

However, as of November 2023, neither g++, Clang, nor MSVC is able to compile reliably. You can use the `lib_ranges_to_container` macro to check if the compiler supports ranges::to.

Using the from_range marker as a constructor parameter, it also works directly with the range in C++23.

```cpp
// https://godbolt.org/z/veovKc8KJ
// as before ...
auto out = in
views::filter([](const int i) { return i%3 == 0; })
views::transform([](const int i) { return i*i; });
vector<int> result(from_range, out);
```
**Listing 24.7** *The range marker also exists only since C++23.*

## 24.1.7 Ranges, Views, Concepts, Adapters, Generators, and Algorithms

The ranges library is located in the <ranges> header, contains the std::ranges namespace, and is divided into several areas:

- Ranges
A range is essentially anything that can be iterated over, has a start, and potentially an end, called sentinel. A typical range is based on a data area—for example, a container—and you can also modify the elements through the range.

- Views
A view is a range and is defined by operations it wants to perform on the elements, such as filtering or transforming the elements. Views are lazy, performing operations only when necessary.

- Concepts
The ranges library defines, for example, the `input_range` concept, which you can use in function parameters.

- Converter
If you use ranges::to (C++23), a view is converted into a container.

- Factories
Factories are views that do not rely on underlying data but generate values—for example, `iota_view`, `empty_view`, or `cartesian_product_view` (C++23).

- Adapter
An adapter takes a range and produces a specific type from it. For example, the reverse adapter produces a `reverse_view`. Typically, you use adapters with the pipe operator |.

- Generators
With `ranges::generator`, you can use coroutines.

- Algorithms
Most algorithms that previously worked with containers are now also defined for ranges. They always work eagerly (i.e., not lazy). You can find them in the <algorithm> header in the std::ranges namespace. They are called constrained algorithms there.
