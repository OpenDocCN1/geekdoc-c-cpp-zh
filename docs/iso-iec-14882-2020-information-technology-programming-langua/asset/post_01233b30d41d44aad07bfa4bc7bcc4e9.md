
the assignment of a non-singular value to an iterator that holds a singular value, and, for iterators that meet the Cpp17DefaultConstructible requirements, using a value-initialized iterator as the source of a copy or move operation.

> [Note 2: This guarantee is not offered for default-initialization, although the distinction only matters for types with trivial default constructors such as pointers or aggregates holding pointers. — end note]

In these cases the singular value is overwritten the same way as any other value. Dereferenceable values are always non-singular.

8 Most of the library's algorithmic templates that operate on data structures have interfaces that use ranges. A range is an iterator and a sentinel that designate the beginning and end of the computation, or an iterator and a count that designate the beginning and the number of elements to which the computation is to be applied.²³⁴

9 An iterator and a sentinel denoting a range are comparable. A range [i, s) is empty if i == s; otherwise, [i, s) refers to the elements in the data structure starting with the element pointed to by i and up to but not including the element, if any, pointed to by the first iterator j such that j == s.

10 A sentinel s is called reachable from an iterator i if and only if there is a finite sequence of applications of the expression ++i that makes i == s. If s is reachable from i, [i, s) denotes a valid range.

11 A counted range i + [0, n) is empty if n == 0; otherwise, i + [0, n) refers to the n elements in the data structure starting with the element pointed to by i and up to but not including the element, if any, pointed to by the result of n applications of ++i. A counted range i + [0, n) is valid if and only if n == 0; or n is positive, i is dereferenceable, and ++i + [0, --n) is valid.

12 The result of the application of library functions to invalid ranges is undefined.

13 All the categories of iterators require only those functions that are realizable for a given category in constant time (amortized). Therefore, requirement tables and concept definitions for the iterators do not specify complexity.

14 Destruction of a non-forward iterator may invalidate pointers and references previously obtained from that iterator.

15 An invalid iterator is an iterator that may be singular.²³⁵

16 Iterators are called constexpr iterators if all operations provided to meet iterator category requirements are constexpr functions.

> [Note 3: For example, the types “pointer to int” and reverse_iterator<int*> are constexpr iterators. — end note]

234) The sentinel denoting the end of a range can have the same type as the iterator denoting the beginning of the range, or a different type.

235) This definition applies to pointers, since pointers are iterators. The effect of dereferencing an iterator that has been invalidated is undefined.

## 23.3.2 Associated types [iterator.assoc.types]

### 23.3.2.1 Incrementable traits [incrementable.traits]

1 To implement algorithms only in terms of incrementable types, it is often necessary to determine the difference type that corresponds to a particular incrementable type. Accordingly, it is required that if WI is the name of a type that models the weakly_incrementable concept (23.3.4.4), the type `iter_difference_t<WI>` be defined as the incrementable type’s difference type.

```
namespace std {
  template<class> struct incrementable_traits { };

  template<class T>
    requires is_object_v<T>
  struct incrementable_traits<T*> {
    using difference_type = ptrdiff_t;
  };

  template<class I>
  struct incrementable_traits<const I>
    : incrementable_traits<I> { };
}
```

```
template<class T>
    requires requires { typename T::difference_type; }
struct incrementable_traits<T> {
    using difference_type = typename T::difference_type;
};
```

```
template<class T>
    requires (!requires { typename T::difference_type; } &&
        requires(const T& a, const T& b) { { a - b } -> integral; })
struct incrementable_traits<T> {
    using difference_type = make_signed_t<decltype(declval<T>() - declval<T>())>;
};
```

```
template<class T>
    using iter_difference_t = see below;
```

2 Let R_I be remove_cvref_t<I>. The type `iter_difference_t<I>` denotes

- `incrementable_traits<R_I>::difference_type` if `iterator_traits<R_I>` names a specialization generated from the primary template, and
- `iterator_traits<R_I>::difference_type` otherwise.

3 Users may specialize `incrementable_traits` on program-defined types.

### 23.3.2.2 Indirectly readable traits [readable.traits]

1 To implement algorithms only in terms of indirectly readable types, it is often necessary to determine the value type that corresponds to a particular indirectly readable type. Accordingly, it is required that if R is the name of a type that models the indirectly_readable concept (23.3.4.2), the type `iter_value_t<R>` be defined as the indirectly readable type's value type.

```
template<class> struct cond-value-type { };    // exposition only
template<class T>
requires is_object_v<T>
struct cond-value-type<T> {
    using value_type = remove_cv_t<T>;
};
```

```
template<class> struct indirectly_readable_traits { };
```

```
template<class T>
struct indirectly_readable_traits<T*>
    : cond-value-type<T> { };
```

```
template<class I>
    requires is_array_v<I>
struct indirectly_readable_traits<I> {
    using value_type = remove_cv_t<remove_extent_t<I>>;
};
```

```
template<class I>
struct indirectly_readable_traits<const I>
    : indirectly_readable_traits<I> { };
```

```
template<class T>
    requires requires { typename T::value_type; }
struct indirectly_readable_traits<T>
    : cond-value-type<typename T::value_type> { };
```

```
template<class T>
    requires requires { typename T::element_type; }
struct indirectly_readable_traits<T>
    : cond-value-type<typename T::element_type> { };
```

```
template<class I, class T>
  concept output_iterator =
    input_or_output_iterator<I> &&
    indirectly_writable<I, T> &&
    requires(I i, T&& t) {
      *i++ = std::forward<T>(t);      // not required to be equality-preserving
    };
```

2 Let E be an expression such that decltype((E)) is T, and let i be a dereferenceable object of type I. I and T model output_iterator<I, T> only if *i++ = E; has effects equivalent to:

  *i = E;
  ++i;

3 Recommended practice: The implementation of an algorithm on output iterators should never attempt to pass through the same iterator twice; such an algorithm should be a single-pass algorithm.

### 23.3.4.11 Concept forward_iterator [iterator.concept.forward]

1 The forward_iterator concept adds copyability, equality comparison, and the multi-pass guarantee, specified below.

```
template<class I>
  concept forward_iterator =
    input_iterator<I> &&
    derived_from<ITER_CONCEPT(I), forward_iterator_tag> &&
    incrementable<I> &&
    sentinel_for<I, I>;
```

2 The domain of == for forward iterators is that of iterators over the same underlying sequence. However, value-initialized iterators of the same type may be compared and shall compare equal to other value-initialized iterators of the same type.

> [Note 1: Value-initialized iterators behave as if they refer past the end of the same empty sequence. — end note]

3 Pointers and references obtained from a forward iterator into a range [i, s) shall remain valid while [i, s) continues to denote a range.

4 Two dereferenceable iterators a and b of type X offer the multi-pass guarantee if:

- (4.1) — a == b implies ++a == ++b and
- (4.2) — the expression ((void)[](X x){++x;}(a), *a) is equivalent to the expression *a.

> [Note 2: The requirement that a == b implies ++a == ++b and the removal of the restrictions on the number of assignments through a mutable iterator (which applies to output iterators) allow the use of multi-pass one-directional algorithms with forward iterators. — end note]

### 23.3.4.12 Concept bidirectional_iterator [iterator.concept.bidir]

1 The bidirectional_iterator concept adds the ability to move an iterator backward as well as forward.

```
template<class I>
  concept bidirectional_iterator =
    forward_iterator<I> &&
    derived_from<ITER_CONCEPT(I), bidirectional_iterator_tag> &&
    requires(I i) {
      { --i } -> same_as<I&>;
      { i-- } -> same_as<I>;
    };
```

2 A bidirectional iterator r is decrementable if and only if there exists some q such that ++q == r. Decrementable iterators r shall be in the domain of the expressions --r and r--.

3 Let a and b be equal objects of type I. I models bidirectional_iterator only if:

- (3.1) — If a and b are decrementable, then all of the following are true:
  - (3.1.1) — addressof(--a) == addressof(a)
  - (3.1.2) — bool(a-- == b)
  - (3.1.3) — after evaluating both a-- and --b, bool(a == b) is still true
  - (3.1.4) — bool(++(--a) == b)
