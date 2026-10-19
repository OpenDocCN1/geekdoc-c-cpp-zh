# 24.3.14 ranges::cdata [range.prim.cdata]

1 The name ranges::cdata denotes a customization point object (16.3.3.3.6). The expression ranges::cdata(E) for a subexpression E of type T is expression-equivalent to:

+   - ranges::data(static_cast<const T&>(E)) if E is an lvalue.
+   - Otherwise, ranges::data(static_cast<const T&&>(E)).

2 [Note 1: Whenever ranges::cdata(E) is a valid expression, it has pointer to object type. — end note]

# 24.4 Range requirements [range.req]

# 24.4.1 General [range.req.general]

1 Ranges are an abstraction that allow a C++ program to operate on elements of data structures uniformly. Calling ranges::begin on a range returns an object whose type models input_or_output_iterator (23.3.4.6). Calling ranges::end on a range returns an object whose type S, together with the type I of the object returned by ranges::begin, models sentinel_for<S, I>. The library formalizes the interfaces, semantics, and complexity of ranges to enable algorithms and range adaptors that work efficiently on different types of sequences.

2 The range concept requires that ranges::begin and ranges::end return an iterator and a sentinel, respectively. The sized_range concept refines range with the requirement that ranges::size be amortized O(1). The view concept specifies requirements on a range type with constant-time destruction and move operations.

3 Several refinements of range group requirements that arise frequently in concepts and algorithms. Common ranges are ranges for which ranges::begin and ranges::end return objects of the same type. Random access ranges are ranges for which ranges::begin returns a type that models random_access_iterator (23.3.4.13). (Contiguous, bidirectional, forward, input, and output ranges are defined similarly.) Viewable ranges can be converted to views.

# 24.4.2 Ranges [range.range]

1 The range concept defines the requirements of a type that allows iteration over its elements by providing an iterator and sentinel that denote the elements of the range.

```
template<class T>
  concept range =
    requires(T& t) {
      ranges::begin(t);
      ranges::end(t);
    };
// sometimes equality-preserving (see below)
```

2 The required expressions ranges::begin(t) and ranges::end(t) of the range concept do not require implicit expression variations (18.2).

3 Given an expression t such that decltype((t)) is T&, T models range only if

+   (3.1) — [ranges::begin(t), ranges::end(t)) denotes a range (23.3.1),
+   (3.2) — both ranges::begin(t) and ranges::end(t) are amortized constant time and non-modifying, and
+   (3.3) — if the type of ranges::begin(t) models forward_iterator, ranges::begin(t) is equality-preserving.

4 [Note 1: Equality preservation of both ranges::begin and ranges::end enables passing a range whose iterator type models forward_iterator to multiple algorithms and making multiple passes over the range by repeated calls to ranges::begin and ranges::end. Since ranges::begin is not required to be equality-preserving when the return type does not model forward_iterator, it is possible for repeated calls to not return equal values or to not be well-defined. — end note]

```
template<class T>
  concept borrowed_range =
    range<T> &&
    (is_lvalue_reference_v<T> || enable_borrowed_range<remove_cvref_t<T>>);
```

5 Given an expression E such that decltype((E)) is T, T models borrowed_range only if the validity of iterators obtained from the object denoted by E is not tied to the lifetime of that object.