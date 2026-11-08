Unfortunately, this introduces a seemingly serious problem for the `largest()` function we created in `Ex9_03.cpp`. To refresh your memory, here is its declaration:

```
```cpp
// double largest(const std::vector<double>& data);
// double largest(const double data[], size_t count);
double largest(std::span<double> data);
```
```

Because a `span<double>` cannot be created from a const vector, `Ex9_03`'s `largest()` function is actually not a proper replacement for the original two function overloads at all. For instance, with `my_const_vector` defined as earlier in this section, the following invocation will not work:

```
```cpp
auto max = largest(my_const_vector);  // Does not compile!
```
```

Luckily, this is easy to solve. To replace `const vector<T>&`, you should use `span<const T>` instead of `span<T>`. That is, you should use a span of const elements. All element accessor functions of a `span<const T>` (including the `[]` operator) return const `T&` references, even if the original array or container was non-const. This is illustrated by the following snippet.

```
```cpp
std::vector<double> my_vector{ 4, 8, 15, 16, 23, 42 };
std::span<const double> my_const_span(my_vector);
// my_const_span[3] = 100;          // Does not compile!
```
```

> **Note**  A `std::string_view` is thus most similar to a `std::span<const char>`. The key difference of course is that `std::string_view` offers extra member functions tailored to working with strings.

The correct prototype for the `largest()` function is therefore as follows:

```
```cpp
double largest(std::span<const double> data);
```
```

Beyond its signature, no other changes are required to the function's definition. You can find the resulting program in `Ex9_03A.cpp`.

> **Tip**  Use `span<const T>` instead of `const vector<T>&`. Similarly, use `span<T>` instead of `vector<T>&`, unless you need to insert or remove elements.

# Fixed-Size Spans

You can also use the `span<>` class template to write a generic function that can operate on fixed-size arrays. All you have to do is add this fixed size as a second argument to the template. You could for instance replace the different `average10()` functions of `Ex8_09A`, `Ex8_09B`, and `Ex8_09C` with a single function as follows:

```
```cpp
// double average10(const double (&values)[10]);
// double average10(const std::array<double, 10>& values);
double average10(std::span<const double, 10> values);
```
```