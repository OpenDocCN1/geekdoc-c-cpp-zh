
## CHAPTER 21 CONSTRAINED TEMPLATES AND CONCEPTS

In essence, these standard concepts are built similarly to ours. `std::random_access_iterator<>`, for instance, is defined in terms of `std::bidirectional_iterator<>` and `std::totally_ordered<>`, where the latter combines all typical requirements for a type’s `<`, `>`, `<=`, `>=`, `!=`, and `==` operators. Yet overall the concepts of the Standard Library will be better / more refined than those that we worked out thus far. They underwent thorough scrutiny during standardization and were perfected along many iterations, and by learning from real-world use of earlier prototypes. Hence our advice:

> **Tip** Whenever possible, use existing concepts defined by the Standard Library or other established libraries. Not just for consistency and interoperability, but also because writing useful concepts is deceptively hard and can take many iterations to get exactly right.

By our count the C++20 Standard Library offers about 100 concepts, far more than we can reasonably cover in this book. Instead we conclude this section with a brief overview of the most important categories of concepts, and in which modules you can find them. Throughout the remainder of this chapter and its exercises we also try to give at least one example from each of the most commonly used categories. For a full list of all concepts and detailed specifications, however, you should consult a Standard Library reference.

The `<concepts>` module offers core language concepts (`same_as<>`, `derived_from<>`, `convertible_to<>`, ...), arithmetic concepts (`integral<>`, `floating_point<>`, ...), concepts for common object operations (`copyable<>`, `assignable_from<>`, `default_initializable<>`, ...), comparison concepts (`totally_ordered<>`, `equality_comparable<>`, ...), and concepts for function-like entities (`invocable<>`, `predicate<>`, `equivalence_relation<>`, ...). If you are not specifically working with either iterators or ranges, `<concepts>` is the best place to start your quest for appropriate concepts.

The `<iterator>` module offers a wide range of iterator concepts (`input_or_output_iterator<>`, `forward_iterator<>`, `random_access_iterator<>`, ...), indirect variations of some concepts from `<concepts>` (`indirectly_copyable<>`, `indirectly_binary_predicate<>`, ...), as well as other common requirements for iterator-based algorithms (`swappable<>`, `sortable<>`, ...). Generally speaking, `indirect_concept<Iter>` is equivalent to `concept<iter_value_t<Iter>>`, where `iter_value_t<Iter>` results in the type of the value that an iterator of type `Iter` points to. Other type traits offered by the `<iterator>` module that are useful when defining iterator requirements include `projected<>` and `iter_difference_t<>`.

The `<ranges>` module, finally, rather unsurprisingly offers the `range<>` and `view<>` concepts, as well as various refinements thereof. Many of the refinements of `range<>` mirror those of the related iterator concepts: `input_range<>`, `bidirectional_range<>`, and so on.

> **Note** Our `String<>` concept has no direct equivalent in the Standard Library, no doubt because most string algorithms can easily be generalized to accept any range, and not just ranges of characters. Algorithms such as the classical Boyer-Moore string search algorithm, for instance, are generalized by the Standard Library in such a way that they could in principle operate on any range (see `std::search()` and `std::boyer_moore_searcher<>`).

### Requires Clauses

You can constrain template type parameters by adding a *requires* clause in between the template parameter list and the template’s body. Combined, the template’s parameter list and optional *requires* clause form the *template head*. The general outline for a constrained template thus becomes as follows:

```cpp
template <parameter list> requires constraints
template body;
```

The constraints component in a template’s requires clause is completely analogous to that of a concept definition (or that of a nested requirement in a requires expression for that matter). It is, in other words, a conjunction or disjunction of one or more constant expressions of type bool.

As a first basic example we constrain an old favorite from Chapter 10: the larger<> template.

```cpp
template <typename T> requires constraints
const T& larger(const T& a, const T& b) { return a > b ? a : b; }
```

You always begin by analyzing what the requirements are of a template. Syntactically, larger<T>() only requires two things: That you can compare two values of type T using the > operator, and that the result of this comparison is implicitly convertible to bool. A first (rarely good) option is to then encode precisely those requirements as a so-called *ad hoc constraint* directly in the template’s requires clause:

```cpp
template <typename T> requires requires (T x) { { x > x } -> std::convertible_to<bool>; }
const T& larger(const T& a, const T& b) { return a > b ? a : b; }
```

The keyword requires appears twice in a row here because we used a requires expression—a constant expression of type bool like any other—in a template’s requires clause.

This particular ad hoc constraint, however, is purely syntactic, and has little to no correlation to any semantic notion. Once your minimal set of requirements are clear, it is therefore typically better to look for suitable concepts that prescribe them (often together with other, related requirements). The standard concept to constrain to types with comparison operators, for instance, is std::totally_ordered<> (part of the <concepts> module).

```cpp
template <typename T> requires std::totally_ordered<T>
const T& larger(const T& a, const T& b) { return a > b ? a : b; }
```

This concept expression adds more requirements than are strictly needed: std::totally_ordered<T> requires all comparison and equality operators of T (<, >, <=, >=, ==, and !=) to behave as expected; not just its > operator. But semantically (mathematically speaking), a total order is precisely what you want for larger<>(): If values of type T are only partially ordered, then there may not be a larger of two values.

> **Note** Speaking of partial orderings, you should know that float, double, and long double also model std::totally_ordered<>, despite the existence of incomparable not-a-number values (see Chapters 4 and 13). From what we can gather, totally_ordered<> implicitly adds the so-called precondition to not pass not-a-number values to the corresponding arguments of the instantiated function. Or, in other words, if T is constrained by totally_ordered<>, the behavior of using not-a-number T values is, at least in principle, undefined. This is perfectly acceptable for our larger<> template, by the way: The notion “larger” loses all meaning when not-a-number values are involved.

Other examples of preconditions are: “do not use numbers that lead to overflow,” “do not use nullptr,” “first <= last,” “do not use graphs with cycles,” and so on. Where concepts constrain types, preconditions constrain values. Even though preconditions are mostly orthogonal to types and concepts (not all operations that operate on the same types will have the same preconditions), totally_ordered<> illustrates that the semantical implications of a concept can bring about preconditions for instantiated templates as well.

In general, imposing more requirements than strictly needed—like we did by requiring std::totally_ordered<> for larger<>()—stimulates the creation of types with predictable, coherent sets of operations, which is something we advocated in the chapter on operator overloading as well. Requiring more than presently needed also ensures that you can still evolve the implementation of a template without having to worry about using operations that are not covered by overly narrow requirements in the template’s head. In general, you want to avoid having to add requirements to the head of a template post factum because doing so might break existing code.

> **Tip** Always specify meaningful semantic requirements. The preferred tools for constraining type parameters are concepts. Properly designed concepts correlate to clean, semantic notions, and therefore impose requirements for complete, coherent sets of operations.

Sometimes requirements involve more than one template parameter. As an example, here is a constrained version of one of the many larger<>() templates of Chapter 10:

```cpp
template <typename T1, typename T2> requires std::totally_ordered_with<T1, T2>
auto&& larger(const T1& a, const T2& b) { return a > b ? a : b; }
```

For types T1 and T2 to model std::totally_ordered_with<>, operators <, ≤, >, ≥, ==, and != should all behave as expected for operands of either type, possibly mixed. Note that this requirement implies that both T1 and T2 must model std::totally_ordered<>.

> **Tip** Try to constrain all template parameters. Unconstrained parameters should be the exception.

#### Shorthand Notation

Up until now, you introduced every template type parameter with the typename keyword (or with the class keyword, of course, when you were feeling frisky). As of C++20, you can instead introduce a type parameter with a type constraint as well. Here is an example:

```cpp
template <std::totally_ordered T>
const T& larger(const T& a, const T& b) { return a > b ? a : b; }
```
