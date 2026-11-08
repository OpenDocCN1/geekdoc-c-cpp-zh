# Compound Requirements

A *compound requirement* is similar to a simple requirement; only besides asserting that a given expression must be valid, a compound requirement can also prohibit this expression from ever throwing an exception and/or constrain the type that it evaluates to. A compound requirement can take the following forms:

```
```cpp
{ expr };                              // expr is a valid expression (same as expr);
{ expr } noexcept;                     // expr is valid and never throws an exception
{ expr } -> type-constraint;           // expr is valid and its type satisfies type-constraint
{ expr } noexcept -> type-constraint;
```
```

The first form, `{ expr };`, is completely equivalent to the corresponding simple requirement. The `noexcept` keyword, however, adds the requirement that `expr` must be known never to throw. In other words, for a `noexcept` requirement to be fulfilled, any function that `expr` invokes must be `noexcept` (either explicitly or implicitly; see Chapter 16). As an example of such a compound requirement, here is a concept for types whose destructors must not throw:

```
```cpp
template <typename T>
concept NoExceptDestructible = requires (T& value) { { value.~T() } noexcept; };
```
```

Because destructors are mostly implicitly `noexcept` (see Chapter 16), nearly all types model `NoExceptDestructible<>`. Note that even fundamental types such as `int` or `double` act as if they have a public destructor, precisely to facilitate generic expressions such as this.

> **Caution** There is no semicolon after the expression inside the curly braces of a compound requirement. As always, there is a semicolon after the complete compound requirement though. Take care not to forget the curly braces around the expression either (especially since `->` can be a valid operator as well!).

The most common use of compound requirements is to constrain the type to which expressions evaluate. In our `RandomAccessIterator<>` example, for instance, it is not enough for the iterators to support all ten required operators; we also expect `i + n` to result in a new iterator, `i < j` to be convertible to `bool`, and so on. With that in mind, here is an updated definition:

```
```cpp
template<class Iter>
concept RandomAccessIterator = BidirectionalIterator<Iter>
    && requires(const Iter i, const Iter j, const int n)
    {
        { i - n } -> std::same_as<Iter>;
        { i + n } -> std::same_as<Iter>;        { n + i } -> std::same_as<Iter>;
        { k + n } -> std::same_as<Iter&>;       { k -= n } -> std::same_as<Iter&>;
        { i[n] } -> std::same_as<decltype(*i)>;
        { i < j } -> std::convertible_to<bool>;
        // ... same for i > j, i <= j, i >= j
    };
```
```

`std::same_as<>` and `std::convertible_to<>` are two of the most commonly used concepts of the `<concepts>` Standard Library module. Being aptly named, their use should be fairly self-explanatory.