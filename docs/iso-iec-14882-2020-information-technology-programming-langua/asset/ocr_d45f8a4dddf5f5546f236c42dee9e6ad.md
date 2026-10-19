# 23.3.5 C++17 iterator requirements [iterator.cpp17]

# 23.3.5.1 General [iterator.cpp17.general]

1 In the following sections, a and b denote values of type X or const X, difference_type and reference refer to the types iterator_traits<X>::difference_type and iterator_traits<X>::reference, respectively, n denotes a value of difference_type, u, tmp, and m denote identifiers, r denotes a value of X&, t denotes a value of value type T, o denotes a value of some type that is writable to the output iterator.

> [Note 1: For an iterator type X there must be an instantiation of iterator_traits<X> (23.3.2.3). — end note]

# 23.3.5.2 Cpp17Iterator [iterator.iterators]

1 The Cpp17Iterator requirements form the basis of the iterator taxonomy; every iterator meets the Cpp17Iterator requirements. This set of requirements specifies operations for dereferencing and incrementing an iterator. Most algorithms will require additional operations to read (23.3.5.3) or write (23.3.5.4) values, or to provide a richer set of iterator movements (23.3.5.5, 23.3.5.6, 23.3.5.7).

2 A type X meets the Cpp17Iterator requirements if:

+   (2.1) — X meets the Cpp17CopyConstructible, Cpp17CopyAssignable, and Cpp17Destructible requirements (16.4.4.2) and lvalues of type X are swappable (16.4.4.3), and
+   (2.2) — iterator_traits<X>::difference_type is a signed integer type or void, and
+   (2.3) — the expressions in Table 84 are valid and have the indicated semantics.

# Table 84: Cpp17Iterator requirements [tab:iterator]

| Expression | Return type | Operational semantics | Assertion/note pre-/post-condition |
|---|---|---|---|
| *r | unspecified |  | Preconditions: r is dereferenceable. |
| ++r | X& |  |  |

# 23.3.5.3 Input iterators [input.iterators]

1 A class or pointer type X meets the requirements of an input iterator for the value type T if X meets the Cpp17Iterator (23.3.5.2) and Cpp17EqualityComparable (Table 25) requirements and the expressions in Table 85 are valid and have the indicated semantics.

2 In Table 85, the term the domain of == is used in the ordinary mathematical sense to denote the set of values over which == is (required to be) defined. This set can change over time. Each algorithm places additional requirements on the domain of == for the iterator values it uses. These requirements can be inferred from the uses that algorithm makes of == and !=.

> [Example 1: The call find(a,b,x) is defined only if the value of a has the property p defined as follows: b has property p and a value i has property p if (*i==x) or if (*i!=x and ++i has property p). — end example]

# Table 85: Cpp17InputIterator requirements (in addition to Cpp17Iterator) [tab:inputiterator]

| Expression | Return type | Operational semantics | Assertion/note pre-/post-condition |
|---|---|---|---|
| a != b | contextually convertible to bool ! (a == b) |  | Preconditions: (a, b) is in the domain of ==. |
| *a | reference, convertible to T |  | Preconditions: a is dereferenceable. The expression (void)*a, *a is equivalent to *a. If a == b and (a, b) is in the domain of == then *a is equivalent to *b. |
| a->m |  | (*a).m | Preconditions: a is dereferenceable. |