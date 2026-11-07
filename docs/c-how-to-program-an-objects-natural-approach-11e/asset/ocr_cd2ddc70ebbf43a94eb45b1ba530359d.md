```
```cpp
// locate minimum and maximum elements in a2
auto [min, max]{std::ranges::minmax_element(a2)};
std::cout << "a2 minimum and maximum elements: "
          << *min << " and " << *max;
```
```

a2 minimum and maximum elements: 1 and 100

# Structured Bindings

Line 45 uses the **minmax_element_result** returned by **minmax_element** to initialize the variables `min` and `max` using a structured binding declaration.^18,19 This is sometimes referred to as unpacking the elements and can be used to extract into individual variables the elements of a built-in array, `std::array` object, `std::pair` or `std::tuple` (each of which has a size that’s known at compile-time). Structured bindings also can be used to unpack the accessible data members of a struct or class object. In each Chapter 13 example in which a function returned a `std::pair`, we also could have used structured bindings to unpack its members.

# transform Algorithm

Lines 51–52 use the C++20 **std::ranges::transform** algorithm to transform the elements of its **input_range** a1 to new values. Each new value is written into the range specified by the algorithm’s second argument, which must be an output iterator and can point to the same container as the **input_range** or a different container. The function provided as **transform**’s third argument receives a value and returns a new value. There is no guarantee of the order in which this function will be called for the range’s elements, so it should not modify the **input_range**’s elements. To modify the original range’s elements, use the **std::foreach** algorithm.^20

```
```cpp
// calculate cube of each element in a1; place results in cubes
std::array<int, a1.size()> cubes{};
std::ranges::transform(a1, cubes.begin(),
    [](auto& x) { return x * x * x; });
std::cout << "\na1 values cubed: ";
std::ranges::copy(cubes, output);
std::cout << "\n";
}
```
```

a1 values cubed: 125 64 343 216 27 729 1 512 1000 8

A **transform** overload accepts two **input_ranges**, an output iterator and a function that takes two arguments and returns a result. This version of **transform** passes corre-

+   18. “Structured Binding Declaration.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/language/structured_binding.
+   19. Dominik Berner, “Quick and Easy Unpacking in C++ with Structured Bindings.” May 24, 2018. Accessed April 18, 2023. https://dominikk.com/structured-bindings/.
+   20. “Algorithms Library—mutating Sequence Operations—Transform.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/alg.transform.