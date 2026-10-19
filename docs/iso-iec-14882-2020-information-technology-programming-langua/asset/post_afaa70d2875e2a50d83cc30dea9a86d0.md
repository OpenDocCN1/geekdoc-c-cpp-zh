
(3.2) — If a and b are incrementable, then bool(--(++a) == b).

## 23.3.4.13 Concept random_access_iterator [iterator.concept.random.access]

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

- (2.1) — (a += n) is equal to b.
- (2.2) — addressof(a += n) is equal to addressof(a).
- (2.3) — (a + n) is equal to (a += n).
- (2.4) — For any two positive values x and y of type D, if (a + D(x + y)) is valid, then (a + D(x + y)) is equal to ((a + x) + y).
- (2.5) — (a + D(0)) is equal to a.
- (2.6) — If (a + D(n - 1)) is valid, then (a + n) is equal to [](I c){ return ++c; }(a + D(n - 1)).
- (2.7) — (b += D(-n)) is equal to a.
- (2.8) — (b -= n) is equal to a.
- (2.9) — addressof(b -= n) is equal to addressof(b).
- (2.10) — (b - n) is equal to (b -= n).
- (2.11) — If b is dereferenceable, then a[n] is valid and is equal to *b.
- (2.12) — bool(a <= b) is true.

## 23.3.4.14 Concept contiguous_iterator [iterator.concept.contiguous]

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

- (2.1) — to_address(a) == addressof(*a),
- (2.2) — to_address(b) == to_address(a) + D(b - a), and
- (2.3) — to_address(c) == to_address(a) + D(c - a).

## 23.3.5 C++17 iterator requirements [iterator.cpp17]

### 23.3.5.1 General [iterator.cpp17.general]

1 In the following sections, a and b denote values of type X or const X, difference_type and reference refer to the types iterator_traits<X>::difference_type and iterator_traits<X>::reference, respectively, n denotes a value of difference_type, u, tmp, and m denote identifiers, r denotes a value of X&, t denotes a value of value type T, o denotes a value of some type that is writable to the output iterator.

> [Note 1: For an iterator type X there must be an instantiation of iterator_traits<X> (23.3.2.3). — end note]

### 23.3.5.2 Cpp17Iterator [iterator.iterators]

1 The Cpp17Iterator requirements form the basis of the iterator taxonomy; every iterator meets the Cpp17Iterator requirements. This set of requirements specifies operations for dereferencing and incrementing an iterator. Most algorithms will require additional operations to read (23.3.5.3) or write (23.3.5.4) values, or to provide a richer set of iterator movements (23.3.5.5, 23.3.5.6, 23.3.5.7).

2 A type X meets the Cpp17Iterator requirements if:

- (2.1) — X meets the Cpp17CopyConstructible, Cpp17CopyAssignable, and Cpp17Destructible requirements (16.4.4.2) and lvalues of type X are swappable (16.4.4.3), and
- (2.2) — iterator_traits<X>::difference_type is a signed integer type or void, and
- (2.3) — the expressions in Table 84 are valid and have the indicated semantics.

# Table 84: Cpp17Iterator requirements [tab:iterator]

| Expression | Return type | Operational semantics | Assertion/note pre-/post-condition |
|---|---|---|---|
| *r | unspecified |  | Preconditions: r is dereferenceable. |
| ++r | X& |  |  |

### 23.3.5.3 Input iterators [input.iterators]

1 A class or pointer type X meets the requirements of an input iterator for the value type T if X meets the Cpp17Iterator (23.3.5.2) and Cpp17EqualityComparable (Table 25) requirements and the expressions in Table 85 are valid and have the indicated semantics.

2 In Table 85, the term the domain of == is used in the ordinary mathematical sense to denote the set of values over which == is (required to be) defined. This set can change over time. Each algorithm places additional requirements on the domain of == for the iterator values it uses. These requirements can be inferred from the uses that algorithm makes of == and !=.

> [Example 1: The call find(a,b,x) is defined only if the value of a has the property p defined as follows: b has property p and a value i has property p if (*i==x) or if (*i!=x and ++i has property p). — end example]

# Table 85: Cpp17InputIterator requirements (in addition to Cpp17Iterator) [tab:inputiterator]

| Expression | Return type | Operational semantics | Assertion/note pre-/post-condition |
|---|---|---|---|
| a != b | contextually convertible to bool ! (a == b) |  | Preconditions: (a, b) is in the domain of ==. |
| *a | reference, convertible to T |  | Preconditions: a is dereferenceable. The expression (void)*a, *a is equivalent to *a. If a == b and (a, b) is in the domain of == then *a is equivalent to *b. |
| a->m |  | (*a).m | Preconditions: a is dereferenceable. |
| ++r | X& |  | Preconditions: r is dereferenceable. Postconditions: r is dereferenceable or r is past-the-end; any copies of the previous value of r are no longer required to be dereferenceable nor to be in the domain of ==. |
| (void)r++ |  |  | equivalent to (void)++r |
| *r++ | convertible to T | { T tmp = *r; ++r; return tmp; } |  |

3 Recommended practice: The implementation of an algorithm on input iterators should never attempt to pass through the same iterator twice; such an algorithm should be a single pass algorithm.

> [Note 1: For input iterators, a == b does not imply ++a == ++b. (Equality does not guarantee the substitution property or referential transparency.) Value type T is not required to be a Cpp17CopyAssignable type (Table 31). Such an algorithm can be used with istreams as the source of the input data through the istream_iterator class template. — end note]

### 23.3.5.4 Output iterators [output.iterators]

1 A class or pointer type X meets the requirements of an output iterator if X meets the Cpp17Iterator requirements (23.3.5.2) and the expressions in Table 86 are valid and have the indicated semantics.

# Table 86: Cpp17OutputIterator requirements (in addition to Cpp17Iterator) [tab:outputiterator]

| Expression | Return type | Operational semantics | Assertion/note pre-/post-condition |
|---|---|---|---|
| *r = o | result is not used |  | Remarks: After this operation r is not required to be dereferenceable. Postconditions: r is incrementable. |
| ++r | X& |  | addressof(r) == addressof(++r). Remarks: After this operation r is not required to be dereferenceable. Postconditions: r is incrementable. |
| r++ | convertible to const X& | { X tmp = r; ++r; return tmp; } | Remarks: After this operation r is not required to be dereferenceable. Postconditions: r is incrementable. |
| *r++ = o | result is not used |  | Remarks: After this operation r is not required to be dereferenceable. Postconditions: r is incrementable. |

# ISO/IEC 14882:2020(E)

Table 85: Cpp17InputIterator requirements (in addition to Cpp17Iterator) (continued)

| Expression | Return type | Operational semantics | Assertion/note pre-/post-condition |
|---|---|---|---|
| ++r | X& |  | Preconditions: r is dereferenceable. Postconditions: r is dereferenceable or r is past-the-end; any copies of the previous value of r are no longer required to be dereferenceable nor to be in the domain of ==. |
| (void)r++ |  |  | equivalent to (void)++r |
| *r++ | convertible to T | { T tmp = *r; ++r; return tmp; } |  |
