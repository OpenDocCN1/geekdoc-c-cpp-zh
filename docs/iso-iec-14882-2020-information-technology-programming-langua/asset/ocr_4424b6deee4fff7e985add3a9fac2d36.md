(3.2) — If a and b are incrementable, then bool(--(++a) == b).

# 23.3.4.13 Concept random_access_iterator [iterator.concept.random.access]

1 The random_access_iterator concept adds support for constant-time advancement with +=, +, -=, and -, as well as the computation of distance in constant time with -. Random access iterators also support array notation via subscripting.

```
template<class I>
concept random_access_iterator =
    bidirectional_iterator<I> &&
    derived_from<ITER_CONCEPT(I), random_access_iterator_tag> &&
    totally_ordered<I> &&
    sized_sentinel_for<I, I> &&
    requires(I i, const I j, const iter_difference_t<I> n) {
        { i += n } -> same_as<I&>;
        { j + n } -> same_as<I>;
        { n + j } -> same_as<I>;
        { i -= n } -> same_as<I&>;
        { j - n } -> same_as<I>;
        { j[n] } -> same_as<iter_reference_t<I>>;
    };
```

2 Let a and b be valid iterators of type I such that b is reachable from a after n applications of ++a, let D be iter_difference_t<I>, and let n denote a value of type D. I models random_access_iterator only if

+   (2.1) — (a += n) is equal to b.
+   (2.2) — addressof(a += n) is equal to addressof(a).
+   (2.3) — (a + n) is equal to (a += n).
+   (2.4) — For any two positive values x and y of type D, if (a + D(x + y)) is valid, then (a + D(x + y)) is equal to ((a + x) + y).
+   (2.5) — (a + D(0)) is equal to a.
+   (2.6) — If (a + D(n - 1)) is valid, then (a + n) is equal to [](I c){ return ++c; }(a + D(n - 1)).
+   (2.7) — (b += D(-n)) is equal to a.
+   (2.8) — (b -= n) is equal to a.
+   (2.9) — addressof(b -= n) is equal to addressof(b).
+   (2.10) — (b - n) is equal to (b -= n).
+   (2.11) — If b is dereferenceable, then a[n] is valid and is equal to *b.
+   (2.12) — bool(a <= b) is true.

# 23.3.4.14 Concept contiguous_iterator [iterator.concept.contiguous]

1 The contiguous_iterator concept provides a guarantee that the denoted elements are stored contiguously in memory.

```
template<class I>
concept contiguous_iterator =
    random_access_iterator<I> &&
    derived_from<ITER_CONCEPT(I), contiguous_iterator_tag> &&
    is_lvalue_reference_v<iter_reference_t<I>> &&
    same_as<iter_value_t<I>, remove_cvref_t<iter_reference_t<I>>> &&
    requires(const I& i) {
        { to_address(i) } -> same_as<add_pointer_t<iter_reference_t<I>>>;
    };
```

2 Let a and b be dereferenceable iterators and c be a non-dereferenceable iterator of type I such that b is reachable from a and c is reachable from b, and let D be iter_difference_t<I>. The type I models contiguous_iterator only if

+   (2.1) — to_address(a) == addressof(*a),
+   (2.2) — to_address(b) == to_address(a) + D(b - a), and
+   (2.3) — to_address(c) == to_address(a) + D(c - a).